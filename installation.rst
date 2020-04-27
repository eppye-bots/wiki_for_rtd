Install
=======

Bots works on operating systems with python installed. Confirmed is:

* windows (windows10, XP, Vista, windows7, Server 2008, Server 2012, etc)
* apple OS.X
* linux debian (ubuntu, mint, etc)
* linux Red hat (Centos. Fedora)
* OpenSolaris
* FreeBSD
* AIX


Windows using bots installer
----------------------------

#. Install Python
    #. Check if Python is already installed.
    #. Use python 2.7; Python >= 3.0 does not work.
    #. Download `Python installer <http://www.Python.org>`_.
    #. Install python (double-click).
#. Install bots
    #. Download `bots installer <http://sourceforge.net/projects/bots/files/bots%20open%20source%20edi%20software/>`_.
    #. Install bots (double-click).
    #. Installation takes some time; be patient. During the installation the libraries bots needs are installed.
    #. You will be notified if the installation went OK.
    #. If not: contact is via the `mailing list <http://groups.google.com/group/botsmail/topics>`_.

.. note::

    #. Mind your rights. Both Python and Bots need to be installed as admin (windows vista/7/8/10).
    #. The windows installer includes libraries for standard installation. Additional libraries/ are needed for eg. SFTP, web API. Best option for installation of additional libraries is using ``pip``, see below.


Install using pip
-----------------

    .. code-block:: console

        $ sudo pip install 'django<1.8'
        $ sudo pip install 'cherrypy<8.0'
        $ sudo pip install genshi
        $ wget -O bots-3.2.0.tar.gz http://sourceforge.net/projects/bots/files/bots%20open%20source%20edi%20software/3.2.0/bots-3.2.0.tar.gz/download
        $ tar -xf bots-3.2.0.tar.gz
        $ cd bots-3.2.0
        $ sudo python setup.py install
        $ cd ..
        #set rigths for bots directory to non-root:
        $ sudo chown -R myusername /usr/lib/python2.7/site-packages/bots

        #start up bots-webserver:
        $ bots-webserver.py


\*nix installation
------------------

There is no ``*.deb`` or ``*.rpm`` for bots.
So a standard python source code install is done.

#. Install Python
    #. Check if Python is already installed - most of the time python is already installed on ``*nix``. Use python 2.6 or 2.7. (not python >= 3.0).
    #. If not: use package manager or see python web site.
#. Install dependencies/libraries
    * See `list of dependencies <#dependencies>`_.
    * Easiest is to use your package manager for installing.
#. Install bots
    #. Download `bots installer <http://sourceforge.net/projects/bots/files/bots%20open%20source%20edi%20software/>`_ (e.g. bots-3.1.0.tar.gz)
    #. Unpack (command-line): ``tar bots-3.1.0.tar.gz``
    #. Go to created directory (command-line): ``cd bots-3.1.0``
    #. Install (command-line): ``python setup.py install``
    #. Postinstall: depending on what do want: change rights for directories botssys, usersys and config or place these elsewhere and make symbolic links in the bots installation directories.

.. note::
    Change the owner/rights for directories botssys, usersys and config.
    Another option is to move these directois to other place and use symbolic links in bots isntallation.


Installation from scratch
-------------------------

Installation on amazon EC2, looks like red hat version of linux

    .. code-block:: console

        #install django
        $ wget -O django.tar.gz https://www.djangoproject.com/download/1.7.11/tarball/
        $ tar -xf django.tar.gz
        $ cd Django-1.7.11
        $ sudo python setup.py install
        $ cd ..
        #install cherrypy
        $ wget http://download.cherrypy.org/CherryPy/3.2.2/CherryPy-3.2.2.tar.gz
        $ tar -xf CherryPy-3.2.2.tar.gz
        $ cd CherryPy-3.2.2
        $ sudo python setup.py install
        $ cd ..
        #install Genshi
        $ wget http://ftp.edgewall.com/pub/genshi/Genshi-0.7.tar.gz
        $ tar -xf Genshi-0.7.tar.gz
        $ cd Genshi-0.7
        $ sudo python setup.py install
        $ cd ..
        #install bots
        $ wget -O bots-3.2.0.tar.gz http://sourceforge.net/projects/bots/files/bots%20open%20source%20edi%20software/3.2.0/bots-3.2.0.tar.gz/download
        $ tar -xf bots-3.2.0.tar.gz
        $ cd bots-3.2.0
        $ sudo python setup.py install
        $ cd ..
        #set rigths for bots directory to non-root:
        $ sudo chown -R myusername /usr/lib/python2.7/site-packages/bots

        #start up bots-webserver:
        $ bots-webserver.py




Dependencies
------------

Always:

    * Needs: 2.7    Python >= 3.0 does not work.
    * Needs: django < 1.8
    * Needs: cherrypy < 8.0

Optional:

    * Genshi (when using templates/mapping to HTML).
    * SFTP needs paramiko.
    * Cdecimals speeds up bots. See `website <http://www.bytereef.org/mpdecimal/index.html>`_
    * bots-dirmonitor needs:

        * pyinotify on ``*nix``
        * Python for Windows extensions (pywin) for windows

    * xlrd (when using incoming editype 'excel').
    * mysql-Python >= 1.2.2, MySQL (when using database MySQL).
    * psycopg2, PostgreSQL (when using database PostgreSQL).


Install FAQ
-----------

.. include:: faq/installfaq.rst
    :start-line: 2
