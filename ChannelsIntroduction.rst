Channel introduction
====================

Channels take care of communication: file I/O, ftp, email, etc. A
channel is either incoming or outgoing. Examples of channels:

.. raw:: html

   <ul><li>

receive email from a pop3-mailbox

.. raw:: html

   </li><li>

send to a ftp-server

.. raw:: html

   </li><li>

pick up in-house invoices from a directory on your computer

.. raw:: html

   </li><li>

put orders in a file queue for import in your application.

.. raw:: html

   </li></ul>

   <blockquote>

Example of communication channels for bots:

.. raw:: html

   </blockquote>

Notes on naming conventions:

.. raw:: html

   <ul><li>

incoming = incoming to bots

.. raw:: html

   </li><li>

outgoing = going out bots

.. raw:: html

   </li><li>

inbound = my organization receives

.. raw:: html

   </li><li>

outbound = going out of my organization

.. raw:: html

   </li></ul>

Note: Bots does client communicates (no server). If you need a
communication server (eg for ftp, as2), use a separate server.

