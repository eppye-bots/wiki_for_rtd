Mapping recipes
===============

.. raw:: html

   <h2>

multiple messages in an edi-file, not split up

.. raw:: html

   </h2>

(a grammar without nextmessage)

.. raw:: html

   <ul><li>

Using inn.get() gives an error: that "root" of incoming message is
empty, etc.

.. raw:: html

   </li><li>

You start the mapping script with getloop(); and do get() with results
of getloop()

.. raw:: html

   </li></ul>

.. raw:: html

   <h2>

Csv messages consisting of only one record type

.. raw:: html

   </h2>
   <ul><li>

use nextmessageblock() to separate the messages

.. raw:: html

   </li><li>

see plugin ...
