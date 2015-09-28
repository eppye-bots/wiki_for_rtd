Nextmessage
-----------

The nextmessage section of a grammar is used to split the messages in an
edi-file; this way a mapping script receives one message at a time.

Example:

.. raw:: html

   <pre><code>structure=    [<br>
   {ID:'ENV',MIN:1,MAX:999,LEVEL:[         #envelope record     <br>
       {ID:'HEA',MIN:1,MAX:9999,LEVEL:[    #header record<br>
           {ID:'LIN',MIN:0,MAX:9999},      #line record<br>
           ]},<br>
       ]}<br>
   ]<br>
   <br>
   nextmessage = ({'BOTSID':'ENV'},{'BOTSID':'HEA'})<br>
   </code></pre>

Using this 'nextmessage' the mapping script receives one HEA-record with
the LIN-records under it. The sender and receiver of the envelope can be
accessed via QUERIES.
