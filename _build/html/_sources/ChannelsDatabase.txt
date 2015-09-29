Direct database communication
-----------------------------

Bots can read and write from a database. See plugin
demo\_databasecommunication on the bots sourceforge site.

.. raw:: html

   <h3>

Discussion: direct database communication or not

.. raw:: html

   </h3>

In most edi setups there is no direct database communication, but an
intermediate file is used:

.. raw:: html

   <ul><li>

inbound edi: bots translates edi files to your import format

.. raw:: html

   </li><li>

outbound edi: the export files of your application are translated by
bots to the wished edi format.

.. raw:: html

   </li></ul>

 Reasons to set up edi using an intermediate file:

.. raw:: html

   <ul><li>

it is better to do the import/export with the tools you are familiar
with, and not to use a new tool (knowledge, maintenance).

.. raw:: html

   </li><li>

different edi partners do use different standards (dialects of the
standards, different interpretations, different countries, different
sectors, edi standards are not that good). Try to use one import/export
format; let the edi software handle the differences between partners.

.. raw:: html

   </li></ul>

 Reasons to use direct database format:

.. raw:: html

   <ul><li>

import/exports are very simple/straightforward

.. raw:: html

   </li><li>

your system does not (yet) have good functionality for handling the
incoming edi data. Example: receive sales reports, but what to do with
this? This data is quite simple, just import this in one (new) table.
The users can query this table for information.

.. raw:: html

   </li></ul>

.. raw:: html

   <h3>

Inbound edi (write to database)

.. raw:: html

   </h3>

   <ul><li>

Translation rule should be to edi-type 'db'

.. raw:: html

   </li><li>

In the mapping script: out.root should be a python object (dict, list,
class, etc); this object is passed to the actual database connector.

.. raw:: html

   </li><li>

Outgoing channel should be type 'db'.

.. raw:: html

   </li><li>

Use a communication script for the outgoing channel
(usersys/communicationscripts/channelname.py). This communication script
does the actual communication with the database.

.. raw:: html

   </li><li>

In the communication script should be 3 functions:

.. raw:: html

   <ul><li>

connect - build database connection.

.. raw:: html

   </li><li>

out-communicate - put the data in the database using the data as
received from the mapping script.

.. raw:: html

   </li><li>

disconnect - close database connection.

.. raw:: html

   </li></ul></li><li>

Use the database connector as needed, eg: python provides by default the
sqlite3 connector, mysql-Python as MySQL database connector, psycopg2 as
PostgreSQL database connector, etc

.. raw:: html

   </li></ul>

.. raw:: html

   <h3>

Outbound edi (read from database)

.. raw:: html

   </h3>
   <ul><li>

Incoming channel should be type 'db'.

.. raw:: html

   </li><li>

Use a communication script for the incoming channel
(usersys/communicationscripts/channelname.py). This communication script
does the actual communication with the database.

.. raw:: html

   </li><li>

In the communication script should be 3 functions:

.. raw:: html

   <ul><li>

connect - build database connection.

.. raw:: html

   </li><li>

incommunicate - fetch the data from the database, send it to the mapping
script.

.. raw:: html

   </li><li>

disconnect - close database connection.

.. raw:: html

   </li></ul></li><li>

Use the database connector as needed, eg: python provides by default the
sqlite3 connector, mysql-Python as MySQL database connector, psycopg2 as
PostgreSQL database connector, etc

.. raw:: html

   </li><li>

Translation should be from edi-type 'db'

.. raw:: html

   </li><li>

In the mapping script: inn.root is the data as received from the
database connector.

.. raw:: html

   </li><li>

Note: the data passed from the communication-script can be any python
object (eg dict, list). If a list (or tuple) is return from the
communication script, bots passes each member of the list as a separate
edi-message to the mapping script.
