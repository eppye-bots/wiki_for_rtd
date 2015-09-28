Calculations and counting in mapping
------------------------------------

Sometimes it is needed to do calculations in mappings. Realize that the
get() functions always return strings, so these strings need to be
converted. Always convert to python's decimals, this is the only way to
avoid rounding errors. More details: pythons decimal documentation

.. raw:: html

   <h3>

Example calculation

.. raw:: html

   </h3>
   <pre><code>import decimal<br>
   <br>
   def main(inn,out):<br>
       TOTAL_AMOUNT = decimal.Decimal('0')         #initialize total amount<br>
       for lin inn.getloop({'BOTSID':'UNH'},{'BOTSID':'LIN'}):<br>
           amount = lin.get({'BOTSID':'LIN'},{'BOTSID':'QTY','1234':None}) <br>
           TOTAL_AMOUNT += decimal.Decimal(amount)   #add amount to TOTAL_AMOUNT<br>
     <br>
       #convert TOTAL_AMOUNT back to string, indicating the number of decimals to be used (precision)      <br>
       total_amount = TOTAL_AMOUNT.quantize(decimal.Decimal('1.00'))   #2 decimals precision<br>
   </code></pre>

Bots version 3.1 has a new method getdecimal(); code above can now be:

.. raw:: html

   <pre><code>import decimal<br>
   <br>
   def main(inn,out):<br>
       TOTAL_AMOUNT = decimal.Decimal('0')         #initialize total amount<br>
       for lin inn.getloop({'BOTSID':'UNH'},{'BOTSID':'LIN'}):<br>
           TOTAL_AMOUNT += lin.getdecimal({'BOTSID':'LIN'},{'BOTSID':'QTY','1234':None})   #add amount to TOTAL_AMOUNT<br>
     <br>
       #convert TOTAL_AMOUNT back to string, indicating the number of decimals to be used (precision)      <br>
       total_amount = TOTAL_AMOUNT.quantize(decimal.Decimal('1.00'))   #2 decimals precision<br>
   </code></pre>

Note: the example above could be done using function getcountsum(), see
below. The recipe above gives you detailed control over the calculation.

.. raw:: html

   <h3>

getcount()

.. raw:: html

   </h3>

returns the number of records in the tree or node. typically used for
UNT-count of segments.

.. raw:: html

   <pre><code>out.getcount() <br>
   #returns the numbers of records in outmessage.<br>
   </code></pre>

   <h3>

getcountoccurrences(mpath)

.. raw:: html

   </h3>

returns the number of records selected by mpath. typically used to count
number of LIN segments.

.. raw:: html

   <pre><code>out.getcountoccurrences({'BOTSID':'UNH'},{'BOTSID':'LIN'}) <br>
   #returns the numbers of LIN-records.<br>
   </code></pre>

   <h3>

getcountsum(mpath)

.. raw:: html

   </h3>

counts the totals value as selected by mpath. typically used to count
total number of ordered articles.

.. raw:: html

   <pre><code>out.getcountsum({'BOTSID':'UNH'},{'BOTSID':'LIN'},{'BOTSID':'QTY','C186.6063':'12','C186.6060':None}) <br>
   #returns total number of ordered articles.<br>
   </code></pre>

