Nextmessageblock
----------------

The nextmessageblock section in a grammar is mostly used for csv-files
consisting of one record-type. Think of excel, where every row has the
same layout. Via nextmessageblock all subsequent records with eg the
same ordernumber are passed as one message to the mapping script. This
is best understood by example: This CSV file:

.. raw:: html

   <pre><code>ordernumber1,buyer1,20120524,1,article1,24<br>
   ordernumber1,buyer1,20120524,2,article2,288<br>
   ordernumber1,buyer1,20120524,3.article3,6<br>
   ordernumber2,buyer2,20120524,1,article5,124<br>
   ordernumber3,buyer1,20120524,1,article1,24<br>
   ordernumber3,buyer1,20120524,2,article4,48<br>
   </code></pre>

has this grammar:

.. raw:: html

   <pre><code>from bots.botsconfig import *<br>
   <br>
   syntax = { <br>
       'field_sep' : ',',               #specify field separator<br>
       'noBOTSID'   : True,             #does not have record-ID's<br>
       }<br>
   <br>
   nextmessageblock = ({'BOTSID':'HEADER','order number':None})   #feed mapping script with separate orders (where ordernumber is different)<br>
   <br>
   structure = [             <br>
   {ID:'HEADER',MIN:1,MAX:9999}         #only 1 record-type<br>
   ]<br>
   <br>
   recorddefs = {<br>
   'HEADER':[    <br>
       ['BOTSID','M',6,'A'],            #Note: BOTSID is ALWAYS needed!<br>
       ['order number', 'M', 17, 'AN'],<br>
       ['buyer ID', 'M', 13, 'AN'],<br>
       ['delivery date', 'C', 8, 'AN'],<br>
       ['line number', 'C', 6, 'N'],<br>
       ['article number', 'M', 13, 'AN'],<br>
       ['quantity', 'M', 20, 'R'],<br>
       ],<br>
   }<br>
   </code></pre>

The mapping script in the translation receives 3 separate orders (so
mapping script will run 3 times):

.. raw:: html

   <pre><code>order with number 1:<br>
   ordernumber1,buyer1,20120524,1,article1,24<br>
   ordernumber1,buyer1,20120524,2,article2,288<br>
   ordernumber1,buyer1,20120524,3.article3,6<br>
   <br>
   order with number 2:<br>
   ordernumber2,buyer2,20120524,1,article5,124<br>
   <br>
   order with number 3:<br>
   ordernumber3,buyer1,20120524,1,article1,24<br>
   ordernumber3,buyer1,20120524,2,article4,48<br>
   </code></pre>

.. raw:: html

   <h3>

Note 1: Use multiple fields for splitting up (bots > 3.1)

.. raw:: html

   </h3>

Example:

.. raw:: html

   <pre><code>nextmessageblock = ([{'BOTSID':'HEADER','order number':None},{'BOTSID':'HEADER','buyer ID':None}])<br>
   </code></pre>

.. raw:: html

   <h3>

Note 2: 'nextmessageblock' works for fixed files with one type of
records (bots > 3.1)

.. raw:: html

   </h3>

