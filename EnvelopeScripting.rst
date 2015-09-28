Envelope scripting
------------------

You can use an envelopescript to do custom enveloping for edifact, x12,
tradacoms, xml.

Exit points that can be used: 1. ta\_infocontent(ta\_info) \* at start
of enveloping process. ta\_info cotains the values that are used to
write the envelope; you can change these values. 1.
envelopecontent(ta\_info,out) \* after bots has built the envelope tree
you can make changes to the envelope tree by using put(), change() etc.

 Functions should be in
bots/usersys/envelopescripts/<editype>/<editype>.py, eg:

.. raw:: html

   <ul><li>

bots/usersys/envelopescripts/edifact/edifact.py

.. raw:: html

   </li><li>

bots/usersys/envelopescripts/x12/x12.py

.. raw:: html

   </li></ul>

.. raw:: html

   <h2>

Examples

.. raw:: html

   </h2>
   <h3>

Example 1

.. raw:: html

   </h3>

Note that this affects all outgoing edifact documents. Add conditional
logic if needed. In file
bots/usersys/envelopescripts/edifact/edifact.py:

.. raw:: html

   <pre><code>def envelopecontent(ta_info,out,*args,**kwargs):<br>
       ''' Add extra fields to the edifact envelope.'''<br>
       out.put({'BOTSID':'UNB','S002.0008': 'PARTNER1'}) #Interchange sender internal identification<br>
       out.put({'BOTSID':'UNB','S003.0014': 'PARTNER2'}) #Interchange recipient internal identification<br>
       out.put({'BOTSID':'UNB','0029': 'A'})             #Processing priority code<br>
       out.put({'BOTSID':'UNB','0032': 'EANCOM'})        #Interchange agreement identifier<br>
   </code></pre>

   <h3>

Example 2

.. raw:: html

   </h3>

In file bots/usersys/envelopescripts/edifact/edifact.py:

.. raw:: html

   <pre><code>def ta_infocontent(ta_info,*args,**kwargs):<br>
       ''' function is called before envelope tree is made.<br>
           values in ta_info will be used to create envelope.<br>
       '''<br>
       if ta_info['topartner'] == '1111111111111':<br>
           ta_info['topartner'] = 'XXXXXXXXXXXXXXXXX'<br>
           ta_info['UNB.S003.0014'] = '012345'<br>
   </code></pre>

   <h3>

Example 3

.. raw:: html

   </h3>

In file bots/usersys/envelopescripts/edifact/edifact.py:

.. raw:: html

   <pre><code>def envelopecontent(ta_info,out,*args,**kwargs):<br>
       ''' function is called after envelope tree is made, but not written yet.<br>
           manipulate envelope tree itself.<br>
       '''<br>
       if ta_info['topartner'] == '1111111111111':<br>
           out.change(where=({'BOTSID':'UNB'},),change={'S003.0010': 'XXXXXXXXXXXXXXXXX'}) #field S003.0010 (receiver) is written to envelope tree<br>
           out.put({'BOTSID':'UNB','S003.0014': '012345'}) #field S003.0014 is written to envelope tree<br>
           ta_info['topartner'] = 'XXXXXXXXXXXXXXXXX'      #takes only care of changing the partnerID in bots interface (does not change envelope itself)<br>
   </code></pre>

