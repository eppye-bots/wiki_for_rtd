Composite routes
================

Introduction
------------

A simple route reads the edi files from one inchannel, translates, and
sends the translated files to one outchannel. More flexibility is
offered by the use of composite routes. In a composite route there are
several entries in the routes screen, each with the same 'idroute' but a
different 'seq' (sequence number within route). Each entry (with
different 'seq') is called route-part. Best way to use this is to have
each route-part do one thing; either:

.. raw:: html

   <ul><li>

fetch incoming files; you can fetch files from multiple sources

.. raw:: html

   </li><li>

translate (typically once per route)

.. raw:: html

   </li><li>

send outgoing files to different destinations/partners using filtering
It is advised to set up composite routes this way (using at least 3
route-parts).

.. raw:: html

   </li></ul>

.. raw:: html

   <h2>

Use cases

.. raw:: html

   </h2>
   <ul><li>

Send edi files via ftp where each partner has its own ftp-server.

.. raw:: html

   </li><li>

Confirmations/acknowledgements: acknowledgements for incoming edi-files
are routed back to the sender (filter by editype/messagetype).

.. raw:: html

   </li><li>

Fetch from multiple sources, eg ftp-servers of different partners..

.. raw:: html

   </li><li>

Route to different internal destinations: invoices to another system
than ASN's (filter by messagetype)

.. raw:: html

   </li><li>

Use a VAN, but one partner uses AS2 (filter by partner)

.. raw:: html

   </li><li>

Incoming files are translated multiple times, each message-type goes to
different destination. Eg: translate orders both to in-house file
(import ERP) and an HTML-email (for viewing).

.. raw:: html

   </li></ul>

.. raw:: html

   <h2>

Example plugin

.. raw:: html

   </h2>

Download the plugin demo\_composite\_route This plugin has one composite
route consisting of:

.. raw:: html

   <ul><li>

2 input parts

.. raw:: html

   </li><li>

translate part

.. raw:: html

   </li><li>

3 output parts, using filtering Detailled description here

.. raw:: html

   </li></ul>

.. raw:: html

   <h2>

Filtering for different outchannels

.. raw:: html

   </h2>

You can filter per outchannel; eg send only asn's through this
outchannel. In route-screen (bots-monitor->Configuration->Routes) the
fields used for filtering under 'Filtering for outchannel'. If eg
toeditype=csv, only csv-files will be send over the outchannel. NOTE: if
filtering is not specified, all outgoing files in the route are send
through the outchannel.

.. raw:: html

   <h2>

Schematic

.. raw:: html

   </h2>

Schematic overview of a route consisting of 5 parts: Note:

.. raw:: html

   <ul><li>

if no inchannel in route-part nothing comes in for that route-part.

.. raw:: html

   </li><li>

if 'translate' in a route-part is off, no translation in that
route-part.

.. raw:: html

   </li><li>

if no outchannel in route-part nothing goes out for that route-part.
