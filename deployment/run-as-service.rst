Run as Service/Daemon
=====================

After Bots installation nothing is runnng in the background (service in windows or daemon in linux/unix). Bots has several parts that you may want to run as services/daemons:

* bots-webserver.py
* bots-jobqueueserver.py (if you use this)
* bots-dirmonitor.py (if you use this)

.. note::
    bots-engine is :doc:`scheduled <schedule-bots-engine>`, it is not a daemon/service.


Windows Services
----------------

2 ways to do use bots as a service (after Python and bots are installed):

#. Official way, using sc.exe or srvany.exe. It's the mcrosoft way. I never use this.

#. Much simpler: use `NSSM <http://nssm.cc/>`_


.. note::
    I mostly use the Task Scheduler, option 'begin the task' set to value 'at start-up'. Simple, works fine for me.




Linux Daemons
-------------

.. note::
    I mostly use cron to start up at boot: '@reboot'. Simple, works fine for me.

Below are some examples that run bots-webserver or jobqueserver as a daemon:


**Example 1 systemd**

(google it, quite simple)


**Example 2 SysV init using start-stop-daemon**

.. code-block:: shell

    #! /bin/sh
    #
    # uses 'start-stop-daemon' , which is used in debian/ubuntu
    #
    NAME=bots-webserver
    PIDFILE="/var/run/$NAME.pid"
    DAEMON="/usr/local/bin/bots-webserver.py"
    DAEMON_ARGS="-cconfig"

    case "$1" in
        start)
            echo "Starting "$NAME" "
            start-stop-daemon --start --verbose --background --pidfile $PIDFILE --make-pidfile --startas $DAEMON -- $DAEMON_ARGS
            ;;
        stop)
            echo "Stopping "$NAME" "
            start-stop-daemon --stop --verbose --pidfile $PIDFILE
            rm -f $PIDFILE
            ;;
        restart)
            echo "Restarting "$NAME" "
            start-stop-daemon --stop --verbose --pidfile $PIDFILE
            rm -f $PIDFILE
            sleep 1
            start-stop-daemon --start --verbose --background --pidfile $PIDFILE --make-pidfile --startas $DAEMON -- $DAEMON_ARGS
            ;;
        \*)
            echo "Usage: ""$(basename "$0")"" {start|stop|restart}"
            echo "    Starts the bots webserver as a daemon."
            echo "    Bots-webserver is part of bots open source edi translator (http://bots.sourceforge.net)."
            exit 1
            ;;
    esac

    exit 0


**Example 2 SysV init**

.. code-block:: shell

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
     \*)
      # For invalid arguments, print the usage message.
      echo "Usage: $0 {start|stop|restart|reload|status}"
      exit 2
      ;;
    esac


**Example 4 upstart (Ubuntu)**

.. code-block:: shell

    description "bots web server"
    author "bots@yourmail.com"

    start on runlevel [2345]
    stop on runlevel [!2345]

    respawn

    exec bots-webserver.py

