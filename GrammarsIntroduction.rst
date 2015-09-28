Introduction
------------

    Definition: *A grammar is a description of an edi-message*. A
    grammar describes the records, fields, formats etc of an edi file.
    Bots uses grammars to parse, check and generate edi files. Grammars
    files are independent of the editype: a grammar for a csv files
    looks the same as a grammar for a x12 file. Grammar files are in:
    usersys/grammars/editype/grammar name.py

    .. raw:: html

       </li></ul>

.. raw:: html

   <h3>

Learn grammar by example

.. raw:: html

   </h3>

Best way to get the idea of a grammar is to look at the (simple) example
in the chapter. This CSV file:

.. raw:: html

   <pre><code>HEADER,ordernumber1,buyer1,20120524<br>
   LINE,1,article1,24,description1<br>
   LINE,2,article2,288,<br>
   LINE,3.article3,6,description3<br>
   </code></pre>

has this grammar:

.. raw:: html

   <pre><code><br>
   <br>
   from bots.botsconfig import *        #always needed<br>
   <br>
   syntax = {                           #'syntax' section<br>
   'field_sep' : ',',               #specify field separator<br>
   'charset'   : 'utf-8',           #specify character-set<br>
   }<br>
   <br>
   structure = [                        #'structure' section<br>
   {ID:'HEADER',MIN:1,MAX:999,LEVEL:[   #each order starts with a HEADER record<br>
   {ID:'LINE',MIN:1,MAX:9999},      #nested under the HEADER record are the LINE records, repeat up to 9999 times<br>
   ]}<br>
   ]<br>
   <br>
   recorddefs = {                       #'recorddefs' section<br>
   'HEADER':[                           #specify the fields in the HEADER record<br>
   ['BOTSID','M',6,'A'],            #BOTSID is for the HEADER tag itself<br>
   ['order number', 'M', 17, 'AN'], #for each field specify the format, max length, M(andatory) or C(onditional)<br>
   ['buyer ID', 'M', 13, 'AN'],<br>
   ['delivery date', 'C', 8, 'AN'],<br>
   ],<br>
   'LINE':[<br>
   ['BOTSID','M',6,'A'],<br>
   ['line number', 'C', 6, 'N'],<br>
   ['article number', 'M', 13, 'AN'],<br>
   ['quantity', 'M', 20, 'R'],<br>
   ['description', 'C', 70, 'R'],<br>
   ],<br>
   }<br>
   </code></pre>

The example above is simple, but fully functional.

.. raw:: html

   <h2>

Sections of a grammar

.. raw:: html

   </h2>

A grammar file consists of these sections:

.. raw:: html

   <ul><li>

syntax: parameters for the grammar like field separator, merge or not,
indent xml, etc.

.. raw:: html

   </li><li>

structure: sequence of records in an edi-message: start-record, nested
records, repeats.

.. raw:: html

   </li><li>

recorddefs: fields per record.

.. raw:: html

   </li><li>

nextmessage: to split up an edi file to separate messages.

.. raw:: html

   </li><li>

nextmessageblock: to split up a cvs-file to messages.

.. raw:: html

   </li></ul>

 A section can be reused/imported from another grammar file. Purpose:
better maintenance of grammars. Example: edifact messages from a certain
directory use the same recorddefs/segments:

.. raw:: html

   <pre><code> from recordsD96AUN import recorddefs<br>
   </code></pre>

One edifact grammar consists of four parts. Example:

.. raw:: html

   <ul><li>

edifact.py (contains syntax common to all edifact grammars)

.. raw:: html

   </li><li>

envelope.py (contains envelope structure and recorddefs common to all
edifact grammars)

.. raw:: html

   </li><li>

recordsD96AUN.py (contains recorddefs common to all edifact D96A
grammars)

.. raw:: html

   </li><li>

ORDERSD96AUN.py (contains structure specifically for ORDERS D96A)

.. raw:: html

   </li></ul>

.. raw:: html

   <h2>

Problems for some edifact grammars on sourceforge site

.. raw:: html

   </h2>

Sometimes you might meet this error for a grammar:

.. raw:: html

   <blockquote>

GrammarError: Grammar "...somewhere...", in structure: nesting collision
detected at record "etc etc". This is the case eg with INVRPT D96A. UN
says about this that you have to make additional choices in message;
either you make some segments mandatory or leave out some segment
groups. EANCOM did make such choices in their implementation guidelines.
So: you can not the grammar directly, edit it according to your needs.
This is according to what UN-edifact wants...
