delete(mpath)
~~~~~~~~~~~~~

Delete(s) the record(s) as specified in mpath in the outmessage (and the
records 'under' that record). After deletion, searching stops (if more
than one records exists for this mpath, only the first one is deleted).
For deleting all records (repeating records) use getloop() to access the
loop, and delete within the loop. Returns: if successful, True,
otherwise False.

.. raw:: html

   <pre><code>#delete a message date in a edifact INVOICD96AUNEAN008:<br>
   out.delete({'BOTSID':'UNH'},{'BOTSID':'DTM','C507.2005':'137'}) <br>
   #delete DTM record where field C507.2005 = '137' ; DTM-record is nested under UNH-record.<br>
   </code></pre>

   <pre><code>#delete all ALC segments in edifact message:<br>
   while message.delete({'BOTSID':'UNH'},{'BOTSID':'ALC'}):<br>
       pass<br>
   </code></pre>

Note: If you want to delete a field, you can use the change option and
put as value "None":

.. raw:: html

   <pre><code>lot = lin.get({'BOTSID':'line','batchnumber':None})<br>
   if not lot == None:<br>
       lin.change(where=({'BOTSID':'line','batchnumber':lot},),change={'batchnumber':None})<br>
   #In this case I want to remove a wrong batchnumber from a specific supplier<br>
   <br>
   </code></pre>

   <h3>

change(where=(mpath),change=mpath)

.. raw:: html

   </h3>

Used to change an existing record. 'where' identifies the record,
'change' are the values that will be changed (or added is values do not
exist) in this record. Only one record is changed. This is always the
last record of the where-mpath After change, searching stops (if more
than one records exists for this mpath, only the first one is changed).
For changing all records (repeating records) use getloop() to access the
loop, and change within the loop.

.. raw:: html

   <pre><code>inn.change(where=({'BOTSID':'UNH'},{'BOTSID':'NAD','3035':'DP'}),change={'3035':'ST'}) <br>
   #changed qualifier 'DP' in NAD record to 'ST'<br>
   </code></pre>

Note: where must be a tuple; if you want to change the root of document,
add a comma to make it a tuple.

.. raw:: html

   <pre><code>inn.change(where=({'BOTSID':'UNH'},),change={'S009.0054':'96A'})<br>
   #                                 ^ note comma here<br>
   </code></pre>

