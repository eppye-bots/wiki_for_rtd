How translations work
---------------------

Best understood by looking at this schema: >
|http://wiki.bots.googlecode.com/hg/MappingScheme.png|

.. raw:: html

   </li></ul>

Step-by-step:

.. raw:: html

   <ol><li>

The edi file is lexed and parsed using the grammar.

.. raw:: html

   </li><li>

The message is transformed into a tree structure. This is similar to the
use of DOM in xml. Advantages:

.. raw:: html

   <ul><li>

easy access to message content. This is quite similar to XML-queries or
X-path.

.. raw:: html

   </li><li>

choose the logic for the mapping script that is best fit for the
situation - instead of being forced to 'loop' over incoming message.

.. raw:: html

   </li><li>

Sorting: eg. sort article lines by article number.

.. raw:: html

   </li><li>

Counting: eg. count number of lines, total amounts etc

.. raw:: html

   </li><li>

Access the data you already written in the tree

.. raw:: html

   </li></ul></li><li>

Split the edi file into separate messages (eg one edi file can contain
multiple orders).

.. raw:: html

   </li><li>

Find the right translation for message.

.. raw:: html

   </li><li>

Run the mapping script for message.

.. raw:: html

   </li><li>

Serialize the outmessage-tree to file. This is checked and formatted
according to the grammar of the outgoing message.

.. raw:: html

   </li><li>

Outgoing messages are enveloped and/or merged.

.. |http://wiki.bots.googlecode.com/hg/MappingScheme.png| image:: http://wiki.bots.googlecode.com/hg/MappingScheme.png
