## Linux, Unix installation

There is no `*`.deb or `*`.rpm for bots - would be great if you have experience 
with this and want to give some help.  
So a standard python source code install is done.

1.  Install Python
    1.  Check if Python is already installed - most of the time python
        is already installed on `*`nix. Use python 2.6 or 2.7. (not
        python \>= 3.0).
    2.  If not: use package manager or see python web site.

2.  Install dependencies/libraries
    -   See [list of dependencies](StartInstallDependencies.md).
    -   Easiest is to use your package manager for installing.

3.  Install bots
    1.  Download [bots
        installer](http://sourceforge.net/projects/bots/files/bots%20open%20source%20edi%20software/)
        (e.g. bots-3.1.0.tar.gz)
    2.  Unpack (command-line):
        ` tar bots-3.1.0.tar.gz `
    3.  Go to created directory (command-line):
        ` cd bots-3.1.0 `
    4.  Install (command-line):
        ` python setup.py install `
    5.  Postinstall: depending on what do want: change rights for
        directories botssys, usersys and config or place these elsewhere
        and make symbolic links in the bots installation directories.

Tip: place the directories botssys, usersys and config somewhere else
(out of /usr), change the owner/rights and make symbolic links in the
bots installation to these directories.

### Installation from scratch

(Note that versions might not be correct anymore.)

Installation on amazon EC2, looks like red hat version of linux:

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


### Installation from scratch (bots2.2)

(Note that versions might not be correct anymore.)

Installation on vanilla CentOS6.2 (logged in as root):

    #install django
    wget http://www.djangoproject.com/download/1.3.1/tarball/
    tar -xf Django-1.3.1.tar.gz
    cd Django-1.3.1
    python setup.py install
    cd ..      
    #install cherrypy
    wget http://download.cherrypy.org/CherryPy/3.2.2/CherryPy-3.2.2.tar.gz
    tar -xf CherryPy-3.2.2.tar.gz
    cd CherryPy-3.2.2
    python setup.py install
    cd ..      
    #install Genshi
    wget http://ftp.edgewall.com/pub/genshi/Genshi-0.6.tar.gz
    tar -xf Genshi-0.6.tar.gz
    cd Genshi-0.6
    python setup.py install
    cd ..      
    #install bots
    wget http://sourceforge.net/projects/bots/files/bots%20open%20source%20edi%20software/2.2.1/bots-2.2.1.tar.gz/download
    tar -xf bots-2.2.1.tar.gz
    cd bots-2.2.1
    python setup.py install
    cd .. 
         
    #start up bots-webserver:
    bots-webserver.py
