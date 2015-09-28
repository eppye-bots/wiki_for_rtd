Useful tools for working with Bots
----------------------------------

These are programs you can use in bots development and deployment.
(please add more)

.. raw:: html

   <h2>

Text Editors

.. raw:: html

   </h2>

Any text editor you use should have syntax colouring/highlighting. This
makes it much easier to spot any mistakes. It is also good to be able to
run python to do syntax checks. Also a good search/replace function (eg
to add extra CR/LF in edifact or x12 files).

.. raw:: html

   <ul><li>

EditPlus (Windows) is the editor I have used for many years and so
continued to use it with Python. There are no python syntax files in the
default installation but you can easily download and add them, several
versions are available. You can also add a "user tool" option to run a
python syntax check directly in the editor, and one to run the bots
grammar check.

.. raw:: html

   </li><li>

Scite (Windows, Linux) provides Python syntax highlighting and python
syntax check directly in the editor to check the correctness of Python
scripts.

.. raw:: html

   </li><li>

Geany (Windows, Linux) provides Python syntax highlighting and python
syntax check directly in the editor to check the correctness of Python
scripts. Quite similar to scite, but more fancy eg with spell checking.
Web site calls it an IDE.

.. raw:: html

   </li><li>

TextWrangler (Mac) provides Python syntax highlighting and python syntax
check directly in the editor to check the correctness of Python scripts.
Also quite similar to Scite, very interesting access to remote scripts
via SSH/SFTP.

.. raw:: html

   </li></ul>

.. raw:: html

   <h2>

IDE (Integrated Development Environment)

.. raw:: html

   </h2>

These are a "step up" from just using a text editor. Please add more if
you have anny experience with these.

.. raw:: html

   <ul><li>

Eclipse with PyDev. You just create a project in the bots directory and
edit everything from that folder.

.. raw:: html

   </li></ul>

.. raw:: html

   <h2>

Compare and merge

.. raw:: html

   </h2>

Tool for comparing files and directories, analyse changes and copy code
changes eg between test and production environments.

.. raw:: html

   <ul><li>

Winmerge (Windows)

.. raw:: html

   </li><li>

Meld (linux)

.. raw:: html

   </li><li>

Tkdiff (windows,linux)

.. raw:: html

   </li><li>

KDiff3 (linux)

.. raw:: html

   </li></ul>

.. raw:: html

   <h2>

Database

.. raw:: html

   </h2>
   <ul><li>

SQLite Expert (Windows, Linux) is a database browser tool for SQLite.
Useful for advanced troubleshooting or learning more about Bots internal
workings. You can use SQL commands to do quick updates or create
reports. Note: I use an old version (1.7) as the newer versions are much
larger and slower and offer nothing more useful.

.. raw:: html

   </li><li>

HeidiSQL (Windows) can be used similarly to the above for bots
installations using the MySQL database. A lightweight interface for
managing MySQL and Microsoft SQL databases. It enables you to browse and
edit data, create and edit tables, views, procedures, triggers and
scheduled events. Also, you can export structure and data either to SQL
file, clipboard or to other servers.

.. raw:: html

   </li><li>

MySQL Workbench (multiple platforms) is the full blown MySQL management
toolset. It provides an integrated tools environment for Database Design
& Modeling, SQL Development (replacing MySQL Query Browser) and Database
Administration (replacing MySQL Administrator). The Community (OSS)
Edition is available from this page under the GPL.

.. raw:: html

   </li></ul>

.. raw:: html

   <h2>

Other tools

.. raw:: html

   </h2>
   <ul><li>

IZArc (Windows) is an archive tool that allows you to open bots plugins
(zip files) and easily modify their contents.

.. raw:: html

   </li><li>

BareTail (Windows) is a free real-time log file monitoring tool. It is
useful for watching Bots log files (engine.log, webserver.log etc).
Multiple tabbed interface, colour highlighting, single small program, no
installer.
