Linux Daemons
=============

some examples that run bots-webserver or jobqueserver as a daemon.

Example1
--------

'I have been starting bots-webserver on my Linux (CentOS) servers via an
entry in rc.local and wanted to provide a means to gracefully shut down
the process on reboot. There have been other examples of init scripts
posted which do the trick, but I wanted to put something together that
conformed to LSB. I took an example script I found online and configured
it for the bots.webserver process. Since CentOS doesn't handle pid files
correctly when using LSB functions, I tweaked it to work around the
issue, and it should work on most distributions without a lot of
modification.'

::

    ### BEGIN INIT INFO
    # Provides:          bots-webserver
    # Required-Start:    $remote_fs $network
    # Required-Stop:     $remote_fs $network
    # Default-Start:     2 3 4 5
    # Default-Stop:      0 1 6
    # Short-Description: BOTS webserver daemon
    # Description:       BOTS webserver daemon
    ### END INIT INFO

    # Using the lsb functions to perform the operations.
    . /lib/lsb/init-functions
    # Process name ( For display )
    NAME=bots-webserver
    # Daemon name, where is the actual executable
    DAEMON=/usr/bin/bots-webserver.py
    # pid file for the daemon
    PIDFILE=/var/run/bots-webserver.pid
    # Arguments for the daemon
    ARGS="> /dev/null 2>&1 &"

    # If the daemon is not there, then exit.
    test -x $DAEMON || exit 5

    case $1 in
     start)
      # Checked the PID file exists and check the actual status of process
      if [ -e $PIDFILE ]; then
       pidofproc -p $PIDFILE $DAEMON && status="0" || status="$?"
       # If the status is SUCCESS then don't need to start again.
       if [ $status = "0" ]; then
        log_success_msg "$NAME process is already running"
        exit # Exit
       fi
      fi
      # Start the daemon.
      # Start the daemon with the help of start-stop-daemon
      # Log the message appropriately
      if start_daemon -p $PIDFILE $DAEMON $ARGS; then
       # For older LSB functions that don't handle -p argument correctly (i.e. CentOS)
       if [ ! -e $PIDFILE ]; then
        pidofproc $DAEMON > $PIDFILE
       fi
       log_success_msg "Starting the process $NAME"
      else
       log_failure_msg "Failed to start the process $NAME"
      fi
      ;;
     stop)
      # Stop the daemon.
      if [ -e $PIDFILE ]; then
       pidofproc -p $PIDFILE $DAEMON > /dev/null && status="0" || status="$?"
       if [ "$status" = 0 ]; then
        killproc -p $PIDFILE $DAEMON
        /bin/rm -f $PIDFILE
        log_success_msg "Stoppping the $NAME process"
       fi
      else
       log_warning_msg "$NAME process is not running"
      fi
      ;;
     restart)
      # Restart the daemon.
      $0 stop && sleep 2 && $0 start
      ;;
     status)
      # Check the status of the process.
      if [ -e $PIDFILE ]; then
       pidofproc -p $PIDFILE $DAEMON > /dev/null && log_success_msg "$NAME process is running" && exit 0 || exit $?
      else
       log_warning_msg "$NAME process is not running"
      fi
      ;;
     reload)
      # Reload the process. Basically sending some signal to a daemon to reload
      # it configurations.
      if [ -e $PIDFILE ]; then
       killproc -p $PIDFILE $DAEMON -signal USR1
       log_success_msg "$NAME process reloaded successfully"
      else
       log_failure_msg "$PIDFILE does not exists"
      fi
      ;;
     *)
      # For invalid arguments, print the usage message.
      echo "Usage: $0 {start|stop|restart|reload|status}"
      exit 2
      ;;
    esac

.. raw:: html

   <h2>

Example2

.. raw:: html

   </h2>

Depends on 'start-stop-daemon' , which is used in debian/ubuntu.

.. raw:: html

   <pre><code>#! /bin/sh<br>
   #<br>
   # uses 'start-stop-daemon' , which is used in debian/ubuntu<br>
   #<br>
   NAME=bots-webserver<br>
   PIDFILE="/var/run/$NAME.pid"<br>
   DAEMON="/usr/local/bin/bots-webserver.py"<br>
   DAEMON_ARGS="-cconfig"<br>
   <br>
   case "$1" in<br>
       start)<br>
           echo "Starting "$NAME" "<br>
           start-stop-daemon --start --verbose --background --pidfile $PIDFILE --make-pidfile --startas $DAEMON -- $DAEMON_ARGS<br>
           ;;<br>
       stop)<br>
           echo "Stopping "$NAME" "<br>
           start-stop-daemon --stop --verbose --pidfile $PIDFILE<br>
           rm -f $PIDFILE<br>
           ;;<br>
       restart)<br>
           echo "Restarting "$NAME" "<br>
           start-stop-daemon --stop --verbose --pidfile $PIDFILE<br>
           rm -f $PIDFILE<br>
           sleep 1<br>
           start-stop-daemon --start --verbose --background --pidfile $PIDFILE --make-pidfile --startas $DAEMON -- $DAEMON_ARGS<br>
           ;;<br>
       *)<br>
           echo "Usage: ""$(basename "$0")"" {start|stop|restart}"<br>
           echo "    Starts the bots webserver as a daemon."<br>
           echo "    Bots-webserver is part of bots open source edi translator (http://bots.sourceforge.net)."<br>
           exit 1<br>
           ;;<br>
   esac<br>
   <br>
   exit 0<br>
   </code></pre>

.. raw:: html

   <h2>

Example3

.. raw:: html

   </h2>

A script for starting the job queue server as a upstart in Ubuntu. Add
the following file: /etc/init/bots-jobqueue.conf

.. raw:: html

   <pre><code>description "Bots Job queue server"<br>
   author "bots@yourmail.com"<br>
   <br>
   start on runlevel [2345]<br>
   stop on runlevel [!2345]<br>
   <br>
   respawn<br>
   <br>
   exec bots-jobqueueserver.py<br>
   </code></pre>

