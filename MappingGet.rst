Get data from incoming message
------------------------------

get(mpath)
~~~~~~~~~~

Get 1 field from the incoming message; mpath specifies which field to
get. Returns: string or, if field not found, None

.. raw:: html

   <pre><code>#get the message date from an edifact invoice:<br>
   inn.get({'BOTSID':'UNH'},{'BOTSID':'DTM','C507.2005':'137','C507.2380':None}) <br>
   </code></pre>

Explanation: get field C507.2380 from DTM-record if field C507.2005 is
'137', DTM-record nested under UNH-record. The field to retrieve is
specified as None.

.. raw:: html

   <h3>

getnozero(mpath)

.. raw:: html

   </h3>

Like get(), but: return a numeric string not equal to '0', otherwise
None. Eg useful in fixed records, where a numeric field is often
initialized with zero's.

.. raw:: html

   <h3>

getloop(mpath)

.. raw:: html

   </h3>

For looping over repeated records or record groups. Typical use: loop
over article lines in an order. Returns an object usable with get(); see
example.

.. raw:: html

   <pre><code>#loop over lines in edifact order:<br>
   for lin in inn.getloop({'BOTSID':'UNH'},{'BOTSID':'LIN'}):<br>
       linenumber = lin.get({'BOTSID':'LIN','1082':None})<br>
       articlenumber = lin.get({'BOTSID':'LIN','C212.7140':None})<br>
       quantity = lin.get({'BOTSID':'LIN'},{'BOTSID':'QTY','C186.6063':'21','C186.6060':None})<br>
   </code></pre>

