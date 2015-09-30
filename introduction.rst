   
Get started with bots
=====================

Introduction
------------

First steps
~~~~~~~~~~~

#. Install bots: :ref:`install`
#. Get bots running: `Get bots running <StartGetBotsRunning.md>`__
#. Do the tutorial to get your first configuration running: `Tutorial <StartMyFirstPlugin.md>`__ 
#. Check out the `plugins <http://code.google.com/p/bots/wiki/PluginIntroduction>`__.


Other info on bots
~~~~~~~~~~~~~~~~~~

* Website is on `sourceforge`_. 
* There is an active mailing list. 
* Check the overview of features


Supported OS's
~~~~~~~~~~~~~~~

Bots works on operating systems with python installed. Confirmed is: 

* windows (2000, XP, Vista, windows7, Server 2008, Server 2012, etc)
* apple OS.X 
* linux (debian, ubuntu, mint, red hat, centos, fedora, amazon EC2, etc) 
* OpenSolaris
* FreeBSD
* AIX 

Let us know if it runs (or not) on another OS.



It's hard to get started
~~~~~~~~~~~~~~~~~~~~~~~~

Often people experience a steep learning curve when starting with edi.
One reason is that of lot of knowledge is involved:

* edi standards (edifact, x12, tradacoms, EANCOM etc)
* business processes between you and your edi-partner (logistics!), changes in the business processes
* understand what your edi-partner wants/requires
* edi communication methods (x400, VAN's, AS2 etc)
* imports and exports of your ERP system
* specifics of the edi software.
* etc

It is hard to find good information about edi: standards are not always
free (eg x12 is not free), decent example messages are hard to get and
often if is hard to find good information on Internet. Edi is
traditionally 'closed' and sparse with information. Partly this seems to
be a 'cultural thing', partly because edi existed before Internet,
partly because it is all about business data that is not for the general
public. Don't give up! ;-)) I think everybody who started with edi has
gone through this.



.. _install:
Installation
--------------------


Windows installation
~~~~~~~~~~~~~~~~~~~~

#. Install Python

   #. Check if Python is already installed.
   #. Use python version 2.6 or 2.7; Python >= 3.0 does not work.
   #. Download Python installer from http://www.Python.org
   #. Install python (double-click).

#. Install bots

   #. Download bots installer.
   #. Install bots (double-click).
   #. Installation takes some time; be patient. 
      During the installation the libraries bots needs are installed.
   #. You will be notified if the installation went OK.

.. note:: mind your rights. Both Python and Bots need to be installed as admin (windows vista/7/8). 

.. note:: the windows installer includes dependencies for standard installation; there are more dependencies for less used functions.



\*nix installation
~~~~~~~~~~~~~~~~~~~~~~~~

There is no \*.deb or \*.rpm for bots - would be great if you have experience with this and want to give some help. 

So a standard python source code install is done.

#. Install Python

    #.  Check if Python is already installed - most of the time python is
        already installed on \*nix. Use python 2.6 or 2.7. (not python >= 3.0).
    #.  If not: use package manager or see python web site.

#. Install dependencies/libraries. See :ref:`dependencies`.
#. Install bots

    #.  Download bots installer (e.g. bots-3.1.0.tar.gz)
    #.  Unpack (command-line): ``tar bots-3.1.0.tar.gz``
    #.  Go to created directory (command-line): ``cd bots-3.1.0``
    #.  Install (command-line): ``python setup.py install``
    #.  Postinstall: depending on what do want: 
        change rights for directories botssys, usersys and config or 
        place these elsewhere and make symbolic links in the bots installation directories.

.. tip:: place the directories botssys, usersys and config somewhere else (out of /usr), change the owner/rights and make symbolic links in the bots installation to these directories.


Installation from scratch (on red hat) ::

   #install django
   wget -O django.tar.gz https://www.djangoproject.com/download/1.4.13/tarball/
   tar -xf django.tar.gz
   cd Django-1.4.13
   sudo python setup.py install
   cd ..     
   #install cherrypy
   wget http://download.cherrypy.org/CherryPy/3.2.2/CherryPy-3.2.2.tar.gz
   tar -xf CherryPy-3.2.2.tar.gz
   cd CherryPy-3.2.2
   sudo python setup.py install
   cd ..      
   #install Genshi
   wget http://ftp.edgewall.com/pub/genshi/Genshi-0.7.tar.gz
   tar -xf Genshi-0.7.tar.gz
   cd Genshi-0.7
   sudo python setup.py install
   cd ..      
   #install bots
   wget -O bots-3.1.0.tar.gz http://sourceforge.net/projects/bots/files/bots%20open%20source%20edi%20software/3.1.0/bots-3.1.0.tar.gz/download
   tar -xf bots-3.1.0.tar.gz
   cd bots-3.1.0
   sudo python setup.py install
   cd .. 
   #set rigths for bots directory to non-root:
   sudo chown -R myusername /usr/lib/python2.6/site-packages/bots
    
   #start up bots-webserver:
   bots-webserver.py


.. note:: versions might not be correct anymore.




.. _dependencies:
Dependencies
~~~~~~~~~~~~

Always needed
++++++++++++++

*  Needs: python 2.6/2.7. Python 2.5 works but extra dependencies are needed. Python >= 3.0 does not work.
*  Needs: django >= 1.4.0
*  Needs: cherrypy > 3.1.0


Optional
++++++++

*  Genshi (when using templates/mapping to HTML).
*  SFTP needs paramiko and pycrypto. Newer versions of paramiko also need ecdsa.
*  Cdecimals speeds up bots. See `here <http://www.bytereef.org/mpdecimal/index.html>`__
*  bots-dirmonitor needs: either pyinotify on \*nix or Python for Windows extensions (pywin) for windows
*  xlrd (when using incoming editype 'excel').
*  mysql-Python >= 1.2.2, MySQL (when using database MySQL).
*  psycopg2, PostgreSQL (when using database PostgreSQL).



Get bots running
-----------------------

Main components
~~~~~~~~~~~~~~~~~

#. Bots-monitor: the user interface; the GUI; this is a web interface
   and runs in a web browser like Firefox, Chrome, or Internet Explorer.

    *   Note: bots uses web technology for the interface - but bots does
        NOT communicate to the internet for this. All is on your local computer.
    *   Bots-monitor can be accessed from all workstations in your LAN.
    *   Warning: out-of-the-box bots-monitor uses plain HTTP and is not secure. Advised is either:
   
        *  do not use bots-monitor over a public network (such as Internet)
        *  secure the connection using `HTTPS/SSL <DeploymentHttps.md>`__.

#. Bots-webserver: program that serves web pages to bots-monitor. The bots-webserver has to run in order to use bots-monitor.
#. Bots-engine: this program does the actual edi communication and translation.

   *  Bots-engine does the communications and translations (of eg edifact or x12).
   *  Bots-engine has no user interface (is a batch process).
   *  To view the results of bots-engine, use bots-monitor.
   *  After performing its actions bots-engine stops.


Start bots-monitor (using bots-webserver)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#.  Start bots-webserver; several options:

    *   When bots is installed using with Windows installer use the 'shortcut' to Bots-webserver in your 'Programs' menu.
    *   (\*nix) Command line: ``bots-webserver.py``
    *   (Windows) go to command line and eg : ``c:\python27\python c:\python27\Scripts\bots-webserver.py``

#.  Bots-webserver should stay running (and not disappear). If not, see Start-up FAQ.
#.  View using your Internet browser: 

    *   When bots-webserver runs on the same computer, use address: ``http://localhost:8080``
    *   When accessing bots-monitor over your LAN (bots-webserver runs on another computer) the IP address or DNS name of that computer, e.g.: ``http://192.168.10.10:8080``.

#.  Default login: user name 'bots', password 'botsbots'.



Start bots-engine
~~~~~~~~~~~~~~~~~

There are several ways to start bots-engine:

#.  (windows, \*nix) Start from bots-monitor: bots-monitor->Run->Run (only new)
#.  (\*nix) Command line: bots-engine.py
#.  (Windows, python 2.7) go to command line and: ``c:\python27\python c:\python27\Scripts\bots-engine.py``

The results of what bots-engine has done can be viewed in the
bots-monitor. 

.. note:: if you did not configure of bots to do something, the bots-engine will run but will not do much. To get bots to do something see Tutorial.


