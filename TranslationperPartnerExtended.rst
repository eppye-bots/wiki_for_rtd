Organize partner specific translations using imports
====================================================

Often in edi you need a number of very similar translations for
different partners - the 'many similar yet different mappings' problems.
You want to organize your mapping scripts so that code is not duplicated
many times, creating maintenance problems. A nice approach is:

.. raw:: html

   <ol><li>

create a default mapping.

.. raw:: html

   </li><li>

for some partners you can use the default mapping, for others use a
partner specific translation

.. raw:: html

   </li><li>

the partner-specific mappings import the default mapping and builds upon
that (additional pre- or post-mapping). Note: plugin
'demo\_partnerdependent' at the bots sourceforge site demonstrates the
use of default mappings and imports.

.. raw:: html

   </li></ol>

.. raw:: html

   <h3>

By Example

.. raw:: html

   </h3>

the default mapping Script file 'orders2idoc.py', translates edifact
ORDERS to idoc ORDERS05)

.. raw:: html

   <pre><code>def main(inn,out):<br>
       # Order number<br>
       out.put({'BOTSID':'EDI_DC40'},{'BOTSID':'E1EDK01'},{'BOTSID':'E1EDK02','QUALF':'001',<br>
                                      'BELNR':inn.get({'BOTSID':'UNH'},{'BOTSID':'BGM','C106.1004':None})})<br>
   <br>
       # Buyer name<br>
       out.put({'BOTSID':'EDI_DC40'},{'BOTSID':'E1EDK01'},{'BOTSID':'E1EDKA1','PARVW':'AG',<br>
                                      'BNAME':inn.get({'BOTSID':'UNH'},{'BOTSID':'NAD','3035':'BY','C056.3412':None})})<br>
   <br>
       # blahblahblah.....lots more complex mapping code for the order<br>
   </code></pre>

 the partner specific mapping Script file 'customer2\_orders2idoc.py'
for for customer. The default mapping is mostly OK, but a few changes
are needed:

.. raw:: html

   <pre><code>import orders2idoc             #here the default mapping is imported<br>
   <br>
   def main(inn,out):<br>
       #*** pre-mapping *******************<br>
       # do partner-specific mapping before the default mapping eg to make the incoming order "more standard" :-)<br>
       # In this example:<br>
       #     customer2 sends RFF+PR:BULK to indicate a stock order. Delete this and change to BGM+120<br>
       #     This must be done pre-mapping because we have complex mapping rules based on BGM order type.<br>
       if inn.get({'BOTSID':'UNH'},{'BOTSID':'RFF','C506.1153':'PR','C506.1154':None}) == 'BULK':<br>
           inn.delete({'BOTSID':'UNH'},{'BOTSID':'RFF','C506.1153':'PR','C506.1154':'BULK'})<br>
           inn.change(where=({'BOTSID':'UNH'},{'BOTSID':'BGM'}),change={'C002.1001':'120'})<br>
   <br>
   <br>
       #*** run the default mapping******************<br>
       orders2idoc.main(inn,out)<br>
   <br>
   <br>
       #*** post-mapping *******************<br>
       # Post-mapping to adjust or add to the mapped output.<br>
       # Delete unwanted text that is sent on their orders<br>
       out.delete({'BOTSID':'EDI_DC40'},{'BOTSID':'E1EDK01'},{'BOTSID':'E1EDKT2','TDLINE':'TOTAL EXCL. GST AUD'})<br>
       # Additional mapping: map buyer name from NAD+AB:<br>
       out.put({'BOTSID':'EDI_DC40'},{'BOTSID':'E1EDK01'},{'BOTSID':'E1EDKA1','PARVW':'AG',<br>
               'BNAME':inn.get({'BOTSID':'UNH'},{'BOTSID':'NAD','3035':'AB','C056.3412':None})})<br>
   </code></pre>

 Some details and tips:

.. raw:: html

   <ol><li>

Make the default mapping is as generic as possible (eg. checking
multiple fields).

.. raw:: html

   </li><li>

Do not not put any partner specific implementation mapping in here

.. raw:: html

   </li><li>

All mapping scripts are in the same directory (for the incoming editype)

.. raw:: html

   </li></ol>

.. raw:: html

   <h3>

Plugin

.. raw:: html

   </h3>

Plugin 'demo\_partnerdependent' at the bots sourceforge site
demonstrates the use of default mappings and imports.
