Bots directories, executables and files
=======================================

Where can I find bots on my system?
-----------------------------------

-  Windows (depends upon python version used):

   -  eg. *C:27-packages*

-  Linux, Unix:

   -  */usr/lib/python2.7/site-packages/bots*
   -  */usr/local/lib/python2.7/dist-packages/bots* (Debian, Ubuntu)
      Note: in the main screen (home) of bots-monitor (GUI) you can see
      where the bots-directories are.

      .. raw:: html

         <h2>

      Where are the programs/executable scripts?

      .. raw:: html

         </h2>
         </li></ul>  

      -  Where installed

   -  Windows (depends upon python version used): *C:27*
   -  Linux, Unix eg in */usr/bin/* or */usr/local/bin/*

-  Overview of executables:

   -  bots-webserver.py - serves the html-pages for the bots-monitor.
   -  bots-engine.py - does the actual edi communication and
      translation.
   -  bots-jobqueueserver.py - the jobqueue-server maintains a queue
      with (job-engine) jobs and fires these asap.
   -  bots-job2queue.py - to send jobs to the jobqueueserver
   -  bots-dirmonitor.py - monitors/watches directoriess; if a file is
      placed in a directory, bots-engine stats (via jobqueueserver)
   -  bots-grammarcheck.py - utility to check a grammar.
   -  bots-xml2botsgrammar.py - utility to generate an xml-grammar from
      an xml file.
   -  bots-updatedb.py - for version migrations: updates the database to
      new definition/schema
   -  bots-plugoutindex.py - for version control systems: generate a
      file with the configuration (routes, channels, etc).
      (configuration as in the database). Note: for the usage
      instructions of the executables use 'help', eg:

      ::

          bots-engine.py --help

.. raw:: html

   <h2>

Where are the edi files?

.. raw:: html

   </h2>
   <ul><li>

Incoming and outgoing

.. raw:: html

   <ul><li>

Set this per channel, using 'path' and 'filename'.

.. raw:: html

   </li><li>

Relative path is relative to bots directory, absolute paths are OK.

.. raw:: html

   </li><li>

In the plugins the edi-files are in bots/botssys/infile

.. raw:: html

   </li></ul></li><li>

The archive/backup.

.. raw:: html

   <ul><li>

each communication channel of bots CAN archive the incoming or outgoing
edi messages.

.. raw:: html

   </li><li>

Set this per channel, using 'archivepath'.

.. raw:: html

   </li><li>

The place of the archive can be 'anywhere'. We mostly use
botssys/archive.

.. raw:: html

   </li><li>

Relative path is relative to bots directory, absolute paths are OK.

.. raw:: html

   </li></ul></li><li>

Internal storage of edi data.

.. raw:: html

   <ul><li>

in subdirectories of bots/botssys/data.

.. raw:: html

   </li><li>

this is where the edi files are fetched from by the bots-monitor (the
'filer' module).

.. raw:: html

   </li></ul></li><li>

Cleanup of old files

.. raw:: html

   <ul><li>

bots manages cleanup of archive and internal storage, based on
configuration settings for number of days to keep.

.. raw:: html

   </li><li>

Incoming files are (usually, unless testing) removed by the channel
setting "remove".

.. raw:: html

   </li><li>

Outgoing files are never removed by bots

.. raw:: html

   </li></ul></li></ul>

.. raw:: html

   <h2>

The directory structure within bots directory

.. raw:: html

   </h2>
   <ul><li>

bots: source code (\ *.py, *\ .pyc, \*.pyo)

.. raw:: html

   <ul><li>

bots/botssys: data file, database, etc

.. raw:: html

   <ul><li>

bots/botssys: when installing a plugin bots makes a backup of
configuration here.

.. raw:: html

   </li><li>

bots/botssys/data: internal storage of edi data.

.. raw:: html

   </li><li>

bots/botssys/sqlitedb: database file(s) of SQLite.

.. raw:: html

   </li><li>

bots/botssys/logging: log file(s) for each run of bots-engine.

.. raw:: html

   </li><li>

bots/botssys/infile: plugins place here example edi data

.. raw:: html

   </li><li>

bots/botssys/outfile: plugins place here translated edi data

.. raw:: html

   </li></ul></li><li>

bots/config: configuration files. See also multiple environments.

.. raw:: html

   </li><li>

bots/install: contains an empty sqlite database and default
configuration files.

.. raw:: html

   </li><li>

bots/installwin: (windows) python libraries used during installation.

.. raw:: html

   </li><li>

bots/locale: translation/internationalisation files for use of another
language.

.. raw:: html

   </li><li>

bots/media: static data for bots-webserver (CSS, html, images,
JavaScript)

.. raw:: html

   </li><li>

bots/sql: sql files for initialising a new database.

.. raw:: html

   </li><li>

bots/templates: templates for bots-webserver

.. raw:: html

   </li><li>

bots/templatetags: custom template-tags for use in django.

.. raw:: html

   </li><li>

bots/usersys: user scripts.

.. raw:: html

   <ul><li>

bots/usersys/charsets: e.g. edifact uses its own character-sets.

.. raw:: html

   </li><li>

bots/usersys/communicationscripts: user scripts for communication
(inchannel, outchannel).

.. raw:: html

   </li><li>

bots/usersys/envelopescripts: user scripts for enveloping.

.. raw:: html

   </li><li>

bots/usersys/grammars: grammars of edi-messages; directories per editype
(x12, edifact, tradacoms, etc).

.. raw:: html

   </li><li>

bots/usersys/mappings: mappings scripts; directories per editype
(incoming).

.. raw:: html

   </li><li>

bots/usersys/partners: partner specific syntax for outgoing messages;
directories per editype.

.. raw:: html

   </li><li>

bots/usersys/routescripts: user scripts for running (part of) route.

.. raw:: html

   </li><li>

bots/usersys/codeconversions: for conversions of codes (deprecated).

.. raw:: html

   </li><li>

bots/usersys/dbconnectors: user scripts for communication from/to
database (old database connector, deprecated).
