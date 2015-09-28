Structure
---------

    Definition: *the structure section in a grammar defines the sequence
    of records in a message.*\  A structure is required in a grammar
    except for template grammars. Example of a simple structure:

    .. raw:: html

       <pre><code>structure = [<br>
       {ID:'ENV',MIN:1,MAX:999, LEVEL:[        #envelope record<br>
           {ID:'HEA',MIN:1,MAX:9999,LEVEL:[    #header record<br>
               {ID:'LIN',MIN:0,MAX:9999},      #line record<br>
               ]},<br>
           ]}<br>
       ]<br>
       </code></pre></li></ul>

The example above should be read as: > ENV-record is required; max 999
repeats.

.. raw:: html

   <blockquote>

'Nested' under the ENV-record: HEA-record; per ENV max 9999 HEA-records;
min is 1, so required. Per HEA-record max 9999 LIN-records; the
LIN-record is not required (MIN=0).

.. raw:: html

   </blockquote>

 Example of a more elaborate structure:

.. raw:: html

   <pre><code>structure = [<br>
   {ID:'ENV',MIN:1,MAX:1, LEVEL:[        #envelope record: max one per file<br>
       {ID:'HEA',MIN:1,MAX:9999,LEVEL:[  #header record of messageat least one message per ENV, max 9999 messages<br>
           {ID:'PAR',MIN:2,MAX:10},      #party record<br>
           {ID:'ALC',MIN:0,MAX:9},       #allowances/charges per message<br>
           {ID:'LIN',MIN:0,MAX:9999},    #line record<br>
           ]},<br>
       {ID:'TRL',MIN:1,MAX:1},           #each ENV record has a trailer record<br>
       ]}<br>
   ]<br>
   </code></pre>

.. raw:: html

   <h3>

A structure consists of

.. raw:: html

   </h3>
   <ol><li>

A structure is a nested list of records.

.. raw:: html

   </li><li>

Each record is a python dict.

.. raw:: html

   </li><li>

per record:

.. raw:: html

   <ul><li>

ID: tag of record.

.. raw:: html

   </li><li>

MIN: minimum number of occurrences.

.. raw:: html

   </li><li>

MAX: maximum number of occurrences.

.. raw:: html

   </li><li>

LEVEL (optional): indicate nested record. The nested records are in a
list of records.

.. raw:: html

   </li><li>

QUERIES (optional)

.. raw:: html

   </li><li>

SUBTRANSLATION (optional). Very advanced. Purpose: identify separate
messages within within a standard envelope.

.. raw:: html

   </li></ul></li></ol>

.. raw:: html

   <h3>

QUERIES

.. raw:: html

   </h3>

QUERIES in a structure are used to extract values from edi files before
the mapping script starts. Example of an structure with QUERIES:

.. raw:: html

   <pre><code>structure = [<br>
   {ID:'ENV',MIN:1,MAX:999,                #envelope record<br>
       QUERIES:{<br>
           'frompartner':  {'BOTSID':'ENV','sender':None},   #extract sender from ENV record.<br>
           'topartner':    {'BOTSID':'ENV','receiver':None}, #extract receiver from ENV record.<br>
           'testindicator':({'BOTSID':'ENV'},{'BOTSID':'MESSAGE','test':None}), #extract testindicator from 'deeper' level; note that this is in tuple (with brackets).<br>
           },<br>
       LEVEL:[         <br>
       {ID:'HEA',MIN:1,MAX:9999,LEVEL:[    #header record<br>
           {ID:'LIN',MIN:0,MAX:9999},      #line record<br>
           ]},<br>
       ]}<br>
   ]<br>
   </code></pre>

Use cases of the information extracted by QUERIES: Think of frompartner,
topartner, reference, testindicator etc.

.. raw:: html

   <ol><li>

to choose the right translation (QUERIES can extract frompartner,
topartner, alt)

.. raw:: html

   </li><li>

Update the database.

.. raw:: html

   </li><li>

In a mapping script this information is inn.ta\_info'.

.. raw:: html

   </li><li>

data in the envelope can be accessed in the mapping.

.. raw:: html

   </li><li>

One of the most import uses is the extraction of botskey.

.. raw:: html

   </li><li>

Typical information extracted by QUERIES:

.. raw:: html

   <ul><li>

frompartner

.. raw:: html

   </li><li>

topartner

.. raw:: html

   </li><li>

reference

.. raw:: html

   </li><li>

testindicator

.. raw:: html

   </li><li>

botskey

.. raw:: html

   </li><li>

alt
