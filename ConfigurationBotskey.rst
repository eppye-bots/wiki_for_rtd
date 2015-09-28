Document View
-------------

Bots focuses mostly on edi files. Another useful way of looking at edi
is to view at 'business documents': orders, asn's, invoices etc. Bots
support this, but to have this work satisfactory some configuration
needs to be done. Essential is the use of document numbers (eg order
number, shipment number, invoice number); in bots this is called
'botskey'.

.. raw:: html

   <h3>

Usage

.. raw:: html

   </h3>

Once 'botskey' is set correct for your documents, it can be used for:

.. raw:: html

   <ul><li>

Viewing and searching business documents:

.. raw:: html

   <ul><li>

View last run: bots-monitor->Last run->Document

.. raw:: html

   </li><li>

View all runs: bots-monitor->All run->Document

.. raw:: html

   </li><li>

Select/search for documents: bots-monitor->Select->Document

.. raw:: html

   </li></ul></li><li>

Set output file name in a channel or in a communicationscript

.. raw:: html

   </li></ul>

.. raw:: html

   <h3>

Configure botskey

.. raw:: html

   </h3>

This can be done in two ways:

.. raw:: html

   <ol><li>

Using QUERIES in the grammar of the incoming edi file.

.. raw:: html

   <pre><code># Example: botskey in a simple csv grammar<br>
   structure = [<br>
       {ID:'LIN',MIN:1,MAX:99999,<br>
           QUERIES:{<br>
               'frompartner': ({'BOTSID':'LIN','AccountCode':None}),<br>
               'topartner':   ({'BOTSID':'LIN','CustomerCode':None}),<br>
               'botskey':     ({'BOTSID':'LIN','PurchaseOrderNo':None}),<br>
           },<br>
       }<br>
   ]<br>
   </code></pre>
   </li><li>

In your mapping script.

.. raw:: html

   <pre><code>    out.ta_info['botskey'] = inn.get({'BOTSID':'LIN','PurchaseOrderCode':None})<br>
   </code></pre>

