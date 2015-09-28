Migrate/update to 3.0.0
-----------------------

Introduction
------------

Version 3.0 is a bigger update for bots, view `all
changes <Migrate300#List_of_Changes.md>`__. Overview: 1. Django 1.1 and
1.2 are not supported anymore. Supported are django 1.3 and 1.4. 1.
Settings.py is changed. Advised: use the new settings.py, and do your
customization in the new setting.py (eg for error reports, maybe
database and timezone). 1. The database has changed. A script is
included to change the database. I had no database issues while testing
this migration. 1. lots of changes in bots.ini. The 'old' bots.ini is
OK, but it is advised to use new bots.ini, and do your customizations
there. 1. Excel input: does work; but is now an incoming messagetype and
not via 'preprocessing'. 1. Most user scripts will work; many user
scripts are not needed anymore because the functionality is provided by
bots now. 1. Some functions that may be used in user scripting have
changed: \* botslib.change() -> botslib.changeq(). This function is used
to in processing incoming 997's and CONTRL!! \* botsengine routescripts:
for 'new' runs in routescript botsengine.py called function
postnewrun(routestorun) -> postnew(routestorun) \*
communication.run(idchannel,idroute) ->
communication.run(idchannel,command,idroute). Command is one of:
'new','automaticretrycommunication','resend','rereceive'. \*
transform.run(idchannel,idroute) ->
transform.run(idchannel,command,idroute). Command is one of:
'new','automaticretrycommunication','resend','rereceive'.

My experiences: after changing settings.py and database migration, all
works (except for and issues mentioned above).

.. raw:: html

   <h2>

Summary of procedure

.. raw:: html

   </h2>
   <ol><li>

make a backup!

.. raw:: html

   </li><li>

rename existing installation.

.. raw:: html

   </li><li>

do a fresh install.

.. raw:: html

   </li><li>

copy old data to new installation.

.. raw:: html

   </li><li>

change settings

.. raw:: html

   </li><li>

update the database. Comments:

.. raw:: html

   </li><li>

It is critical to change the settings before updating the database! Bots
finds the right database via the settings!

.. raw:: html

   </li><li>

If you use MySQL or PostGreSQL: same procedure. The bots-updatedb script
also updates MySQL or PostGreSQL.

.. raw:: html

   </li><li>

Tested this for migration from bots2.2.1 -> 3.0.0, but works for all
bots2.\* installations.

.. raw:: html

   </li></ol>

.. raw:: html

   <h2>

Windows procedure

.. raw:: html

   </h2>
   <ol><li>

make a backup!

.. raw:: html

   </li><li>

rename existing installation

.. raw:: html

   <ul><li>

existing bots-installation is in C:27-packages

.. raw:: html

   </li><li>

renamed bots directory to bots221

.. raw:: html

   </li><li>

also renamed existing directories for cherrypy, django, genshi.

.. raw:: html

   </li></ul></li><li>

do a fresh install of bots3.0.0 installer (bots-3.0.0.win32.exe)

.. raw:: html

   </li><li>

copy old data to new installation.

.. raw:: html

   <ul><li>

in C:27-packages new directories have been installed (bots, django,
cherrypy, genshi)

.. raw:: html

   </li><li>

copy directories botssys and usersys from bots221-directory to bots
directories. Everything can be overwritten.

.. raw:: html

   </li></ul></li><li>

change settings

.. raw:: html

   <ul><li>

use new config/bots.ini, adapt for your own values.

.. raw:: html

   </li><li>

use new config/settings.py, adapt for your own values. Especially the
database settings are important; the format is slightly different (but
similar enough to give no problem); critical is using the 'ENGINE'-value
of the new settings.py.

.. raw:: html

   </li></ul></li><li>

update the database.

.. raw:: html

   <ul><li>

use command-prompt/dos-box

.. raw:: html

   </li><li>

goto directory C:27

.. raw:: html

   </li><li>

command-line: C:27bots-updatedb.py

.. raw:: html

   </li><li>

should report that database is successful changed. If you use a 64-bits
version of windows another option is to use the 64-bits versions of
python and bots.

.. raw:: html

   <h2>

Linux procedure

.. raw:: html

   </h2>
   </li></ul></li><li>

make a backup!

.. raw:: html

   </li><li>

rename existing installation

.. raw:: html

   <ul><li>

existing bots-installation is in /usr/local/lib/python2.7/dist-packages

.. raw:: html

   </li><li>

renamed bots directory to bots221

.. raw:: html

   </li><li>

for libraries: check you use at least django 1.3

.. raw:: html

   </li></ul></li><li>

do a fresh install: see installation procedure

.. raw:: html

   </li><li>

copy old data to new installation.

.. raw:: html

   <ul><li>

in /usr/local/lib/python2.7/dist-packages new bots-directory is
installed.

.. raw:: html

   </li><li>

copy directories botssys and usersys from bots221-directory to bots
directories. Everything can be overwritten.

.. raw:: html

   </li><li>

mind your rights!

.. raw:: html

   </li></ul></li><li>

change settings

.. raw:: html

   <ul><li>

use new config/bots.ini, adapt for your own values.

.. raw:: html

   </li><li>

use new config/settings.py, adapt for your own values. Especially the
database settings are important; the format is slightly different (but
similar enough to give no problem); critical is using the 'ENGINE'-value
of the new settings.py.

.. raw:: html

   </li></ul></li><li>

update the database.

.. raw:: html

   <ul><li>

command-line: bots-updatedb.py

.. raw:: html

   </li><li>

should report that database is successful changed.
