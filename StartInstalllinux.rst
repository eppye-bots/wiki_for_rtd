Linux, Unix installation
------------------------

There is no ``*``.deb or ``*``.rpm for bots - would be great if you have
experience with this and want to give some help. So a standard python
source code install is done.

.. raw:: html

   <ol><li>

Install Python

.. raw:: html

   <ol><li>

Check if Python is already installed - most of the time python is
already installed on \*nix. Use python 2.6 or 2.7. (not python >= 3.0).

.. raw:: html

   </li><li>

If not: use package manager or see python web site.

.. raw:: html

   </li></ol></li><li>

Install dependencies/libraries

.. raw:: html

   <ul><li>

See list of dependencies.

.. raw:: html

   </li><li>

Easiest is to use your package manager for installing.

.. raw:: html

   </li></ul></li><li>

Install bots

.. raw:: html

   <ol><li>

Download bots installer (e.g. bots-3.1.0.tar.gz)

.. raw:: html

   </li><li>

Unpack (command-line): tar bots-3.1.0.tar.gz

.. raw:: html

   </li><li>

Go to created directory (command-line): cd bots-3.1.0

.. raw:: html

   </li><li>

Install (command-line): python setup.py install

.. raw:: html

   </li><li>

Postinstall: depending on what do want: change rights for directories
botssys, usersys and config or place these elsewhere and make symbolic
links in the bots installation directories.

.. raw:: html

   </li></ol></li></ol>

Tip: place the directories botssys, usersys and config somewhere else
(out of /usr), change the owner/rights and make symbolic links in the
bots installation to these directories.

.. raw:: html

   <h3>

Installation from scratch

.. raw:: html

   </h3>

(Note that versions might not be correct anymore. Installation on amazon
EC2, looks like red hat version of linux:

.. raw:: html

   <pre><code>#install django<br>
   wget -O django.tar.gz https://www.djangoproject.com/download/1.4.13/tarball/<br>
   tar -xf django.tar.gz<br>
   cd Django-1.4.13<br>
   sudo python setup.py install<br>
   cd ..      <br>
   #install cherrypy<br>
   wget http://download.cherrypy.org/CherryPy/3.2.2/CherryPy-3.2.2.tar.gz<br>
   tar -xf CherryPy-3.2.2.tar.gz<br>
   cd CherryPy-3.2.2<br>
   sudo python setup.py install<br>
   cd ..      <br>
   #install Genshi<br>
   wget http://ftp.edgewall.com/pub/genshi/Genshi-0.7.tar.gz<br>
   tar -xf Genshi-0.7.tar.gz<br>
   cd Genshi-0.7<br>
   sudo python setup.py install<br>
   cd ..      <br>
   #install bots<br>
   wget -O bots-3.1.0.tar.gz http://sourceforge.net/projects/bots/files/bots%20open%20source%20edi%20software/3.1.0/bots-3.1.0.tar.gz/download<br>
   tar -xf bots-3.1.0.tar.gz<br>
   cd bots-3.1.0<br>
   sudo python setup.py install<br>
   cd .. <br>
   #set rigths for bots directory to non-root:<br>
   sudo chown -R myusername /usr/lib/python2.6/site-packages/bots<br>
    <br>
   #start up bots-webserver:<br>
   bots-webserver.py<br>
   </code></pre>

.. raw:: html

   <h3>

Installation from scratch (bots2.2)

.. raw:: html

   </h3>

(Note that versions might not be correct anymore. Installation on
vanilla CentOS6.2 (logged in as root):

.. raw:: html

   <pre><code>#install django<br>
   wget http://www.djangoproject.com/download/1.3.1/tarball/<br>
   tar -xf Django-1.3.1.tar.gz<br>
   cd Django-1.3.1<br>
   python setup.py install<br>
   cd ..      <br>
   #install cherrypy<br>
   wget http://download.cherrypy.org/CherryPy/3.2.2/CherryPy-3.2.2.tar.gz<br>
   tar -xf CherryPy-3.2.2.tar.gz<br>
   cd CherryPy-3.2.2<br>
   python setup.py install<br>
   cd ..      <br>
   #install Genshi<br>
   wget http://ftp.edgewall.com/pub/genshi/Genshi-0.6.tar.gz<br>
   tar -xf Genshi-0.6.tar.gz<br>
   cd Genshi-0.6<br>
   python setup.py install<br>
   cd ..      <br>
   #install bots<br>
   wget http://sourceforge.net/projects/bots/files/bots%20open%20source%20edi%20software/2.2.1/bots-2.2.1.tar.gz/download<br>
   tar -xf bots-2.2.1.tar.gz<br>
   cd bots-2.2.1<br>
   python setup.py install<br>
   cd .. <br>
        <br>
   #start up bots-webserver:<br>
   bots-webserver.py<br>
   </code></pre>

