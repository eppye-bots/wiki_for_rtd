XML namespaces
==============

http://www.w3schools.com/xml/xml\_namespaces.asp

based on mailing list topics
`here <https://groups.google.com/forum/#!topic/botsmail/PtAjn6QApy4>`__
and `here <https://code.google.com/p/bots/w/edit/XMLnamespace>`__

Dealing with xml namespaces can be a bit difficult in Bots. They can
greatly complicate grammars and mappings. Often your EDI partner will
want to send or receive XML with namespaces, but actually Bots does not
need (or want) them as there are rarely any naming conflicts within a
single XML file!

Where an XML file has only one namespace, usually the "default"
namespace is used. eg. xmlns="schemas-hiwg-org-au:EnvelopeV1.0

If the file has multiple namespaces, then namespace prefixes are used.
These prefixes can be any value. eg.
xmlns:ENV="schemas-hiwg-org-au:EnvelopeV1.0"

There are several ways to deal with namespaces in Bots:

.. raw:: html

   <h2>

1. Ignore incoming XML namespace

   .. raw:: html

      </h2>

   For incoming XML files that are to be mapped into something else, you
   probably don't need the namespaces at all. In my opinion this is the
   "best" way. See Ignore incoming XML namespace for an example
   preprocessing script to achieve this.

   .. raw:: html

      <h2>

   2. Use incoming XML namespace

      .. raw:: html

         </h2>

      When a namespace must be used, it is needed in many places
      (structure, recorddefs, mapping) but you want to specify the
      namespace string, which can be quite long, only in one place (DRY
      principle). This has several benefits:

      .. raw:: html

         <ul><li>

      If it needs to change, this is easy to do in one place only

      .. raw:: html

         </li><li>

      grammar and mapping will be smaller, and look neater

      .. raw:: html

         </li></ul>

For example, the incoming XML file may look like ...

.. raw:: html

   <pre><code>&lt;?xml version="1.0"?&gt;<br>
   &lt;Orders xmlns:xsd="http://www.w3.org/2001/XMLSchema"<br>
        xmlns="http://www.company.com/EDIOrders"<br>
        targetNamespace="http//www.company.com/EDIOrders"&gt;<br>
         &lt;Order&gt;<br>
           &lt;OrderNumber&gt;239062415&lt;/OrderNumber&gt;<br>
           &lt;DateOrdered&gt;2014-02-24&lt;/DateOrdered&gt;<br>
           &lt;LineCount&gt;10&lt;/LineCount&gt;<br>
   etc...<br>
   </code></pre>

If you created your grammar with xml2botsgrammar, it probably has the
namespace repeated over and over in structure and recorddefs, like
this...

.. raw:: html

   <pre><code>structure=    [<br>
   {ID:'{http://www.company.com/EDIOrders}Orders',MIN:1,MAX:1,LEVEL:[<br>
       {ID:'{http://www.company.com/EDIOrders}Order',MIN:1,MAX:99999,<br>
           QUERIES:{<br>
                'botskey':      {'BOTSID':'{http://www.company.com/EDIOrders}Order','{http://www.company.com/EDIOrders}OrderNumber':None},<br>
               },<br>
           LEVEL:[<br>
           {ID:'{http://www.company.com/EDIOrders}OrderItems',MIN:0,MAX:1,LEVEL:[<br>
               {ID:'{http://www.company.com/EDIOrders}OrderLine',MIN:1,MAX:99999},<br>
               ]},<br>
           ]},<br>
       ]}<br>
   ]<br>
   <br>
   recorddefs = {<br>
      '{http://www.company.com/EDIOrders}Orders':[<br>
               ['BOTSID','M',256,'A'],<br>
               ['{http://www.company.com/EDIOrders}Orders__targetNamespace','C',256,'AN'],<br>
             ],<br>
      '{http://www.company.com/EDIOrders}Order':[<br>
               ['BOTSID','M',256,'A'],<br>
               ['{http://www.company.com/EDIOrders}OrderNumber','C', 20,'AN'],<br>
               ['{http://www.company.com/EDIOrders}DateOrdered','C', 10,'AN'],<br>
               ['{http://www.company.com/EDIOrders}LineCount','C', 5,'R'],<br>
   <br>
   # etc...<br>
   </code></pre>

So, we want to improve this. In your grammar, first add the namespace as
a string constant. This is the only place it should be specified, and
everywhere else refers to it. Note: If the XML has multiple namespaces,
you can use the same technique and just add more constants (xmlns1,
xmlns2, etc). Also include it in the syntax dict. This allows us to
reference it later in mappings.

.. raw:: html

   <pre><code>xmlns='{http://www.company.com/EDIOrders}'<br>
   <br>
   syntax = {<br>
           'xmlns':xmlns,<br>
   }<br>
   </code></pre>

In your grammar, replace all instances of the namespace string with the
constant, so it looks like this...

.. raw:: html

   <pre><code>structure=    [<br>
   {ID:xmlns+'Orders',MIN:1,MAX:1,LEVEL:[<br>
       {ID:xmlns+'Order',MIN:1,MAX:99999,<br>
           QUERIES:{<br>
                'botskey':      {'BOTSID':xmlns+'Order',xmlns+'OrderNumber':None},<br>
               },<br>
           LEVEL:[<br>
           {ID:xmlns+'OrderItems',MIN:0,MAX:1,LEVEL:[<br>
               {ID:xmlns+'OrderLine',MIN:1,MAX:99999},<br>
               ]},<br>
           ]},<br>
       ]}<br>
   ]<br>
   <br>
   recorddefs = {<br>
      xmlns+'Orders':[<br>
               ['BOTSID','M',256,'A'],<br>
               [xmlns+'Orders__targetNamespace','C',256,'AN'],<br>
             ],<br>
      xmlns+'Order':[<br>
               ['BOTSID','M',256,'A'],<br>
               [xmlns+'OrderNumber','C', 20,'AN'],<br>
               [xmlns+'DateOrdered','C', 10,'AN'],<br>
               [xmlns+'LineCount','C', 5,'R'],<br>
   <br>
   # etc...<br>
   </code></pre>

Now in the mapping script, read the xmlns value from grammar.

.. raw:: html

   <pre><code>import bots.grammar as grammar<br>
   <br>
       xmlns = grammar.grammarread('xml',inn.ta_info['messagetype']).syntax['xmlns']<br>
   </code></pre>

Then use it wherever needed in the mapping, like this...

.. raw:: html

   <pre><code>    # Get OrderNumber from XML with namespace<br>
       OrderNumber = inn.get({'BOTSID':xmlns+'Order',xmlns+'OrderNumber':None})<br>
   </code></pre>

   <h2>

3. Outgoing XML with only a default namespace

   .. raw:: html

      </h2>

This can be done by defining xmlns as a tag, and setting it in mapping.
It eliminates the need to use namespace prefix on every record and
field. example grammar

.. raw:: html

   <pre><code>recorddefs = {<br>
       'shipment':<br>
           [<br>
           ['BOTSID', 'M', 20, 'AN'],<br>
           ['shipment__xmlns', 'C', 80, 'AN'],   # xmlns is added as a tag (note double underscore)<br>
           ['ediCustomerNumber', 'M', 12, 'N'],<br>
           ['ediParm1', 'M', 1, 'N'],<br>
           ['ediParm2', 'M', 1, 'AN'],<br>
           ['ediParm3', 'M', 1, 'AN'],<br>
           ['ediReference', 'M', 35, 'AN'],<br>
           ['ediFunction1', 'M', 3, 'AN'],<br>
           ['ediCustomerSearchName', 'M', 20, 'AN'],<br>
           ],<br>
   }<br>
   </code></pre>

example mapping

.. raw:: html

   <pre><code>    # xmlns tag for shipment<br>
       out.put({'BOTSID':'shipment','shipment__xmlns':'http://www.company.com/logistics/shipment'})<br>
   </code></pre>

example output

.. raw:: html

   <pre><code>&lt;?xml version="1.0" encoding="utf-8" ?&gt;<br>
   &lt;shipment xmlns="http://www.company.com/logistics/shipment"&gt;<br>
       &lt;ediCustomerNumber&gt;191&lt;/ediCustomerNumber&gt;<br>
       &lt;ediParm1&gt;4&lt;/ediParm1&gt;<br>
       &lt;ediParm2&gt;s&lt;/ediParm2&gt;<br>
       &lt;ediParm3&gt;d&lt;/ediParm3&gt;<br>
       &lt;ediReference&gt;SCN1022164911&lt;/ediReference&gt;<br>
       &lt;ediFunction1&gt;9&lt;/ediFunction1&gt;<br>
       &lt;ediCustomerSearchName&gt;SCHA&lt;/ediCustomerSearchName&gt;<br>
   &lt;/shipment&gt;<br>
   </code></pre>

   <h2>

4. Outgoing XML with default namespace prefixes (ns0, ns1, etc)

   .. raw:: html

      </h2>

This is the default behaviour of the python elementtree module used in
Bots. The actual prefix used is not important to XML meaning, so in
theory your EDI partners should not care what prefixes you use. example
grammar

.. raw:: html

   <pre><code>xmlns_env='{schemas-hiwg-org-au:EnvelopeV1.0}'<br>
   xmlns='{schemas-hiwg-org-au:InvoiceV3.0}'<br>
   <br>
   syntax = {<br>
           'xmlns_env':xmlns_env,<br>
           'xmlns':xmlns,<br>
           'merge':False,<br>
           'indented':True,<br>
   }<br>
   <br>
   nextmessage = ({'BOTSID':xmlns_env+'Envelope'},{'BOTSID':'Documents'},{'BOTSID':xmlns+'Invoice'})<br>
   <br>
   structure = [<br>
   {ID:xmlns_env+'Envelope',MIN:0,MAX:99999,<br>
       QUERIES:{<br>
           'frompartner':{'BOTSID':xmlns_env+'Envelope',xmlns_env+'SenderID':None},<br>
           'topartner':{'BOTSID':xmlns_env+'Envelope',xmlns_env+'RecipientID':None},<br>
           },<br>
       LEVEL:[<br>
       {ID:'Documents',MIN:0,MAX:99999,LEVEL:[<br>
           {ID:xmlns+'Invoice',MIN:0,MAX:99999,<br>
               QUERIES:{<br>
                   'botskey':({'BOTSID':xmlns+'Invoice',xmlns+'DocumentNo':None}),<br>
                   },<br>
               LEVEL:[<br>
               {ID:xmlns+'Supplier',MIN:0,MAX:99999},<br>
               {ID:xmlns+'Buyer',MIN:0,MAX:99999},<br>
               {ID:xmlns+'Delivery',MIN:0,MAX:99999},<br>
               {ID:xmlns+'Line',MIN:0,MAX:99999},<br>
               {ID:xmlns+'Trailer',MIN:0,MAX:99999},<br>
           ]},<br>
       ]},<br>
   ]},<br>
   ]<br>
   </code></pre>

example output

.. raw:: html

   <pre><code>&lt;?xml version="1.0" encoding="utf-8" ?&gt;<br>
   &lt;ns0:Envelope xmlns:ns0="schemas-hiwg-org-au:EnvelopeV1.0" xmlns:ns1="schemas-hiwg-org-au:InvoiceV3.0"&gt;<br>
       &lt;ns0:SenderID&gt;sender&lt;/ns0:SenderID&gt;<br>
       &lt;ns0:RecipientID&gt;recipient&lt;/ns0:RecipientID&gt;<br>
       &lt;ns0:DocumentCount&gt;1&lt;/ns0:DocumentCount&gt;<br>
       &lt;Documents&gt;<br>
           &lt;ns1:Invoice&gt;<br>
               &lt;ns1:TradingPartnerID&gt;ID1&lt;/ns1:TradingPartnerID&gt;<br>
               &lt;ns1:MessageType&gt;INVOIC&lt;/ns1:MessageType&gt;<br>
               &lt;ns1:VersionControlNo&gt;3.0&lt;/ns1:VersionControlNo&gt;<br>
               &lt;ns1:DocumentType&gt;TAX INVOICE&lt;/ns1:DocumentType&gt;<br>
   </code></pre>

   <h2>

5. Outgoing XML with specific namespace prefixes

   .. raw:: html

      </h2>

Your EDI partner may request a specific namespace prefix be used; This
is technically un-necessary and bad design, but they may insist on it
anyway! example grammar

.. raw:: html

   <pre><code>xmlns_env='{schemas-hiwg-org-au:EnvelopeV1.0}'<br>
   xmlns='{schemas-hiwg-org-au:InvoiceV3.0}'<br>
   <br>
   syntax = {<br>
           'xmlns_env':xmlns_env,<br>
           'xmlns':xmlns,<br>
           'namespace_prefixes':[('ENV',xmlns_env.strip('{}')),('INV',xmlns.strip('{}'))], # use ENV, INV instead of ns0, ns1<br>
           'merge':False,<br>
           'indented':True,<br>
   }<br>
   <br>
   structure = [<br>
   {ID:xmlns_env+'Envelope',MIN:0,MAX:99999,<br>
       QUERIES:{<br>
           'frompartner':{'BOTSID':xmlns_env+'Envelope',xmlns_env+'SenderID':None},<br>
           'topartner':{'BOTSID':xmlns_env+'Envelope',xmlns_env+'RecipientID':None},<br>
           },<br>
       LEVEL:[<br>
       {ID:'Documents',MIN:0,MAX:99999,LEVEL:[<br>
           {ID:xmlns+'Invoice',MIN:0,MAX:99999,<br>
               QUERIES:{<br>
                   'botskey':({'BOTSID':xmlns+'Invoice',xmlns+'DocumentNo':None}),<br>
                   },<br>
               LEVEL:[<br>
               {ID:xmlns+'Supplier',MIN:0,MAX:99999},<br>
               {ID:xmlns+'Buyer',MIN:0,MAX:99999},<br>
               {ID:xmlns+'Delivery',MIN:0,MAX:99999},<br>
               {ID:xmlns+'Line',MIN:0,MAX:99999},<br>
               {ID:xmlns+'Trailer',MIN:0,MAX:99999},<br>
           ]},<br>
       ]},<br>
   ]},<br>
   ]<br>
   </code></pre>

example output

.. raw:: html

   <pre><code>&lt;?xml version="1.0" encoding="utf-8" ?&gt;<br>
   &lt;ENV:Envelope xmlns:ENV="schemas-hiwg-org-au:EnvelopeV1.0" xmlns:INV="schemas-hiwg-org-au:InvoiceV3.0"&gt;<br>
       &lt;ENV:SenderID&gt;sender&lt;/ENV:SenderID&gt;<br>
       &lt;ENV:RecipientID&gt;recipient&lt;/ENV:RecipientID&gt;<br>
       &lt;ENV:DocumentCount&gt;1&lt;/ENV:DocumentCount&gt;<br>
       &lt;Documents&gt;<br>
           &lt;INV:Invoice&gt;<br>
               &lt;INV:TradingPartnerID&gt;ID1&lt;/INV:TradingPartnerID&gt;<br>
               &lt;INV:MessageType&gt;INVOIC&lt;/INV:MessageType&gt;<br>
               &lt;INV:VersionControlNo&gt;3.0&lt;/INV:VersionControlNo&gt;<br>
               &lt;INV:DocumentType&gt;TAX INVOICE&lt;/INV:DocumentType&gt;<br>
   </code></pre>

