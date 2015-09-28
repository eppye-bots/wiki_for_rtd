Preprocessing and Postprocessing examples
-----------------------------------------

Some recipes for preprocessing edi files. Plugin 'demo\_preprocessing'
at the bots sourceforge site demonstrates preprocessing.

.. raw:: html

   <h3>

Example 1: Discard input files that are too small

.. raw:: html

   </h3>
   <pre><code>import os<br>
   import bots.preprocess as preprocess<br>
   from bots.botsconfig import *<br>
   <br>
   def postincommunication(routedict,*args,**kwargs):<br>
       ''' function is called after the communication in the route.'''<br>
       preprocess.preprocess(routedict=routedict,function=discard_file)<br>
   <br>
   def discard_file(ta_from,endstatus,*args,**kwargs):<br>
       ''' discard files that are to small (zero files)''' <br>
       ta_from.synall()<br>
       filesize = ta_from.filesize<br>
       if filesize &lt; 100:    #filesize in bytes<br>
           ta_from.update(statust=DONE)                       #statust=DONE: bots discards file, gives no errors.<br>
       else:<br>
           ta_to = ta_from.copyta(status=endstatus)           #make new transaction for bots database<br>
           ta_to.update(statust=OK,filename=ta_from.filename) #update outmessage transaction (same) filename<br>
   </code></pre>

.. raw:: html

   <h3>

Example 2: Extract data from PDF file (to csv)

.. raw:: html

   </h3>
   <pre><code># Extract data from PDF file (to csv)<br>
   # x_group: group text closer than this as one field (default 10)<br>
   # y_group: group lines closer than this as one line (default 5)<br>
   # password: if required<br>
   <br>
   import bots.preprocess as preprocess<br>
   <br>
   def postincommunication(routedict,*args,**kwargs):<br>
       preprocess.preprocess(routedict,preprocess.extractpdf,x_group=12,y_group=3,password='secret')<br>
   </code></pre>

.. raw:: html

   <h3>

Example 3: Manipulate records without BOTSID

.. raw:: html

   </h3>
   <pre><code>import bots.preprocess as preprocess<br>
   import bots.botslib as botslib<br>
   import bots.botsglobal as botsglobal<br>
   from bots.botsconfig import *<br>
   <br>
   def postincommunication(routedict,*args,**kwargs):<br>
       preprocess.preprocess(routedict,custom_preprocess)<br>
   <br>
   def custom_preprocess(ta_from,endstatus,*args,**kwargs):<br>
       try:<br>
           # copy ta for preprocessing<br>
           ta_to = ta_from.copyta(status=endstatus)<br>
   <br>
           # open the files<br>
           infile = botslib.opendata(ta_from.filename,'r')<br>
           tofile = botslib.opendata(str(ta_to.idta),'wb')<br>
   <br>
           # preprocessing: read infile, write tofile<br>
           # This file has headers and lines, but no field that can be used for BOTSID!<br>
           # Determine the line type from the data, and add HDR or LIN in first column<br>
           # Text heading lines and blank lines are omitted<br>
           for line in infile:<br>
               if '\tAU' in line: <br>
                   tofile.write('HDR\t' + line)<br>
               elif ('\tWAIT' in line or<br>
                     '\tFULL' in line or<br>
                     '\tEMPTY' in line):<br>
                   tofile.write('LIN\t' + line)<br>
   <br>
           infile.close()<br>
           tofile.close()<br>
   <br>
           ta_to.update(statust=OK,filename=str(ta_to.idta)) #update outmessage transaction with ta_info; <br>
       except:<br>
           txt=botslib.txtexc()<br>
           botsglobal.logger.error(u'Custom preprocess failed. Error:\n%s',txt)<br>
           raise botslib.InMessageError(u'Custom preprocess failed. Error:\n$error',error=txt)<br>
   </code></pre>

.. raw:: html

   <h3>

Example 4: Sort input file

.. raw:: html

   </h3>
   <pre><code>import bots.preprocess as preprocess<br>
   import bots.botslib as botslib<br>
   import bots.botsglobal as botsglobal<br>
   from bots.botsconfig import *<br>
   <br>
   def postincommunication(routedict,*args,**kwargs):<br>
       preprocess.preprocess(routedict,sort_file)<br>
   <br>
   def sort_file(ta_from,endstatus,*args,**kwargs):<br>
       try:<br>
           # copy ta for preprocessing<br>
           ta_to = ta_from.copyta(status=endstatus)<br>
   <br>
           # open the files<br>
           infile = botslib.opendata(ta_from.filename,'r')<br>
           tofile = botslib.opendata(str(ta_to.idta),'wb')<br>
   <br>
           # sort output<br>
           lines = infile.readlines()<br>
           lines.sort()<br>
           for line in lines:<br>
               tofile.write(line)<br>
   <br>
           infile.close()<br>
           tofile.close()<br>
   <br>
           ta_to.update(statust=OK,filename=str(ta_to.idta)) #update outmessage transaction with ta_info; <br>
       except:<br>
           txt=botslib.txtexc()<br>
           botsglobal.logger.error(u'Sort preprocess failed. Error:\n%s',txt)<br>
           raise botslib.InMessageError(u'Sort preprocess failed. Error:\n$error',error=txt)<br>
   </code></pre>

.. raw:: html

   <h3>

Example 5: Postprocessing

.. raw:: html

   </h3>

Post processing works the same way as pre processing, except it is done
before out communication.

.. raw:: html

   <pre><code>import bots.preprocess as preprocess<br>
   import bots.botslib as botslib<br>
   import bots.botsglobal as botsglobal<br>
   from bots.botsconfig import *<br>
   <br>
   def preoutcommunication(routedict,*args,**kwargs):<br>
       preprocess.postprocess(routedict,split_lines)<br>
   <br>
   def split_lines(ta_from,endstatus,,*args,**kwargs):<br>
       try:<br>
           # copy ta for postprocessing, open the files<br>
           ta_to = ta_from.copyta(status=endstatus)<br>
           infile = botslib.opendata(ta_from.filename,'r')<br>
           tofile = botslib.opendata(str(ta_to.idta),'wb')<br>
   <br>
           # split every line at the first separator (space)<br>
           # output the two parts on separate lines<br>
           for line in infile:<br>
               part = line.partition(' ')<br>
               tofile.write(part[0] + '\n' + part[2])<br>
   <br>
           # close files and update outmessage transaction with ta_info<br>
           infile.close()<br>
           tofile.close()<br>
           ta_to.update(statust=OK,filename=str(ta_to.idta))<br>
   <br>
       except:<br>
           txt=botslib.txtexc()<br>
           botsglobal.logger.error(_(u'split_lines postprocess failed. Error:\n%s'),txt)<br>
           raise botslib.OutMessageError(_(u'split_lines postprocess failed. Error:\n$error'),error=txt)<br>
   </code></pre>

.. raw:: html

   <h3>

Example 6: Preprocessing an encrypted file

.. raw:: html

   </h3>

This example uses gnupg to decrypt a file before processing it in Bots.

.. raw:: html

   <pre><code>import bots.preprocess as preprocess<br>
   import bots.botslib as botslib<br>
   import gnupg<br>
   <br>
   # Preprocessing - Decrypt infile using GPG<br>
   # Dependencies: python-gnupg-0.3.0<br>
   #   botssys/gnugpghome directory, containing:<br>
   #     gpg binary files (gpg.exe and iconv.dll)<br>
   #     keys (pubring.gpg, secring.gpg, trustdb.gpg)<br>
   #     passphrase.txt<br>
   <br>
   def postincommunication(routedict,*args,**kwargs):<br>
       # preprocess to decrypt, then passthrough (no translation)<br>
       preprocess.preprocess(routedict,decrypt_GPG)<br>
       transform.addinfo(change={'status':MERGED},where={'status':FILEIN,'idroute':routedict['idroute']})<br>
   <br>
   def decrypt_GPG(ta_from,endstatus,*args,**kwargs):<br>
   <br>
       # copy ta for preprocessing<br>
       ta_to = ta_from.copyta(status=endstatus)<br>
   <br>
       # gnupghome contains the gpg binary files, public/private keys, and passphrase<br>
       gnupghome = botslib.join(botsglobal.ini.get('directories','botssys'),'gnupghome')<br>
       passphrase = open(botslib.join(gnupghome,'passphrase.txt'),'r').read()<br>
       gpgbinary = botslib.join(gnupghome,'gpg.exe')<br>
   <br>
       # Here is where we do the actual decryption<br>
       gpg = gnupg.GPG(gnupghome=gnupghome,gpgbinary=gpgbinary)<br>
       with botslib.opendata(ta_from.filename,'rb') as input:<br>
           status = gpg.decrypt_file(input, passphrase=passphrase,output=botslib.abspathdata(str(ta_to.idta)))<br>
   <br>
       # log the results and finish<br>
       botsglobal.logger.debug(status.stderr)<br>
       if status.ok:<br>
           botsglobal.logger.info(status.status)<br>
           ta_to.update(statust=OK,filename=str(ta_to.idta))<br>
       else:<br>
           botsglobal.logger.error(status.status)<br>
           ta_to.update(statust=ERROR,filename=str(ta_to.idta))<br>
           raise PreprocessError(status.status + '\n' + status.stderr)<br>
   <br>
   class PreprocessError(botslib.BotsError):<br>
       pass<br>
   </code></pre>

.. raw:: html

   <h3>

Example 7: Preprocessing to ignore/remove XML namespaces

.. raw:: html

   </h3>

This example changes the default namespace to a namespace prefix (so it
is ignored). It also removes a namespace prefix (ENV). You may need to
use either or both of these methods, depending on the content of your
XML file.

.. raw:: html

   <pre><code>#-------------------------------------------------------------------------------<br>
   # preprocess - Remove XML namespaces to simplify grammar and mapping<br>
   # Generally Bots does not need to use the xmlns for incoming files<br>
   # This example handles both default and prefix namespaces<br>
   <br>
   def postincommunication(routedict):<br>
   <br>
       def _preprocess(ta_from,endstatus,**argv):<br>
   <br>
           # copy ta for preprocessing<br>
           ta_to = ta_from.copyta(status=endstatus)<br>
   <br>
           # open the files<br>
           infile = botslib.opendata(ta_from.filename,'r')<br>
           tofile = botslib.opendata(str(ta_to.idta),'wb')<br>
   <br>
           for line in infile:<br>
               tofile.write(line.replace('xmlns=','xmlns:NOTUSED=').replace('&lt;ENV:','&lt;').replace('&lt;/ENV:','&lt;/'))<br>
   <br>
           # close files and update outmessage transaction<br>
           infile.close()<br>
           tofile.close()<br>
           ta_to.update(statust=OK,filename=str(ta_to.idta))<br>
   <br>
       preprocess.preprocess(routedict,_preprocess)<br>
   </code></pre>

