Examples for small user exit
----------------------------

.. raw:: html

   <h4>

Filter email attachments

.. raw:: html

   </h4>

Some edi-partners send signatures etc in their email. Script does a
simple check if incoming attachment starts with 'UNB'. (Note: Bots
treats any text in the email body as another "attachment")

.. raw:: html

   <pre><code>def accept_incoming_attachment(channeldict,ta,charset,content,contenttype,*args,**kwargs):<br>
       if 'UNB' in content[0:50]:<br>
           return True   #attachments is OK<br>
       else:<br>
           return False  #skip this attachment<br>
   </code></pre>

.. raw:: html

   <h4>

Set email subject

.. raw:: html

   </h4>

Some edi-partners send signatures etc in their email. By default bots
uses a number for emails. Sometimes you want a more meaningfull subject.

.. raw:: html

   <pre><code>def subject(channeldict,ta,subjectstring,content,*args,**kwargs):<br>
       ta.synall()        #needed to get access to attributes of object ta (eg ta.frompartner)<br>
       return 'EDI messages from ' + ta.frompartner + '_' + subjectstring<br>
   </code></pre>

.. raw:: html

   <h4>

Name archive file same as input file

.. raw:: html

   </h4>

Not needed for bots 3.; do this via setting in bots.ini

.. raw:: html

   <pre><code>import os<br>
   import bots.botslib as botslib<br>
   <br>
   def archivename(channeldict,idta,filename,*args,**kwargs):<br>
        taparent=botslib.OldTransaction(idta=idta)<br>
        ta_list = botslib.trace_origin(ta=taparent,where={'status':EXTERNIN})<br>
        archivename = os.path.basename(ta_list[0].filename)<br>
        return archivename <br>
   </code></pre>

.. raw:: html

   <h4>

Set the archive path

.. raw:: html

   </h4>

Path root is set in channel. Add sub-dir per date, then sub-dir per
channel under it.

.. raw:: html

   <pre><code>import time<br>
   import bots.botslib as botslib<br>
   <br>
   def archivepath(channeldict,*args,**kwargs):<br>
       archivepath = botslib.join(channeldict['archivepath'],time.strftime('%Y%m%d'),channeldict['idchannel'])<br>
       return archivepath<br>
   </code></pre>

.. raw:: html

   <h4>

Partners in the output file name

.. raw:: html

   </h4>

Not needed for bots 3.; do this via file name in GUI

.. raw:: html

   <pre><code>def filename(channeldict,filename,ta,*args,**kwargs):<br>
       ta.synall()        #needed to get access to attributes of object ta (eg ta.frompartner)<br>
       return ta.frompartner + '_' + ta.topartner + '_' + filename<br>
   </code></pre>

.. raw:: html

   <h4>

Name the output file from botskey

.. raw:: html

   </h4>

botskey can be set in grammar or mapping, eg. from customer's order
number. If no botskey is found, the default file naming method will be
used. Syntax must contain 'merge':False. Not needed for bots 3.; do this
via file name in GUI.

.. raw:: html

   <pre><code>def filename(channeldict,filename,ta,*args,**kwargs):<br>
       ta.synall()<br>
       if ta.botskey:<br>
           return filename + ta.botskey<br>
       else:<br>
           return filename<br>
   </code></pre>

.. raw:: html

   <h4>

Name the output file same as input file

.. raw:: html

   </h4>

Syntax must contain 'merge':False. Not needed for bots 3.
