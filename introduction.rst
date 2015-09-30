.. _botswebsite: http://bots.sourceforge.net

Get started with bots
=====================

Introduction
------------

First steps
~~~~~~~~~~~

#. Install bots: :ref:`install`
#. Get bots running: `Get bots running <StartGetBotsRunning.md>`__
#. Get your first configuration running:
   `Tutorial <StartMyFirstPlugin.md>`__ After that: check out some
   `plugins <http://code.google.com/p/bots/wiki/PluginIntroduction>`__.

Other info on bots
~~~~~~~~~~~~~~~~~~

* Website is on `botswebsite`_. 
* Website is on `sourceforge <http://bots.sourceforge.net>`_. 
* There is an active mailing list. 
* Check the overview of features


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

etc


It is hard to find good information about edi: standards are not always
free (eg x12 is not free), decent example messages are hard to get and
often if is hard to find good information on Internet. Edi is
traditionally 'closed' and sparse with information. Partly this seems to
be a 'cultural thing', partly because edi existed before Internet,
partly because it is all about business data that is not for the general
public. Don't give up! ;-)) I think everybody who started with edi has
gone through this.


.. _install:
Install
========


Introduction
------------

Bots works on operating systems with python installed. Confirmed is: 

* windows (2000, XP, Vista, windows7, Server 2008, Server 2012, etc)

* apple OS.X 

* linux (debian, ubuntu, mint, red hat, centos, fedora, etc) 

* OpenSolaris

* FreeBSD

* AIX 

Let us know if it runs (or not) on another OS.



Windows installation
--------------------

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

.. note: mind your rights. Both Python and Bots need to be installed as admin (windows vista/7/8). 
.. note: the windows installer includes dependencies for standard installation; there are more dependencies for less used functions.

