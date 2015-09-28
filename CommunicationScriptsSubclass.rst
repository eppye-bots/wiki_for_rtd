Subclassing communication
-------------------------

It is possible to overwrite bots communication methods completely. This
is done using python subclassing. Again, as with all communication
scripting there should be a file in usersys/communicationscripts with
the same name as the channel (and extension '.py')

.. raw:: html

   <h4>

Example 1

.. raw:: html

   </h4>

In this case communication-type of the channel is 'file'. Bots will
check the communication-script file if there is a class called 'file'
and use that. The class 'file' subclasses the standard 'file' method of
bots.

.. raw:: html

   <pre><code>import bots.communication as communication<br>
   <br>
   class file(communication.file):<br>
       def connect(self,*args,**kwargs):<br>
           #do the preparing work<br>
           print 'in connect method'<br>
   </code></pre>

   <h4>

Example 2

.. raw:: html

   </h4>

In this case communication-type of the channel is 'ftp'. The class 'ftp'
subclasses the standard 'ftp' method of bots. The 'outcommunicate'
method of the ftp class is taken over with this implementation.

.. raw:: html

   <pre><code>import bots.communication as communication<br>
   import bots.botslib as botslib<br>
   from bots.botsconfig import *<br>
   <br>
   class ftp(communication.ftp):<br>
       @botslib.log_session<br>
       def outcommunicate(self,*args,**kwargs):<br>
           #get right filename_mask &amp; determine if fixed name (append) or files with unique names<br>
           filename_mask = self.channeldict['filename'] if self.channeldict['filename'] else '*'<br>
           if '{overwrite}' in filename_mask:<br>
               filename_mask = filename_mask.replace('{overwrite}','')<br>
               mode = 'STOR '<br>
           else:<br>
               mode = 'APPE '<br>
           for row in botslib.query('''SELECT idta,filename,numberofresends<br>
                                       FROM ta<br>
                                       WHERE idta&gt;%(rootidta)s<br>
                                         AND status=%(status)s<br>
                                         AND statust=%(statust)s<br>
                                         AND tochannel=%(tochannel)s<br>
                                           ''',<br>
                                       {'tochannel':self.channeldict['idchannel'],'rootidta':self.rootidta,<br>
                                       'status':FILEOUT,'statust':OK}):<br>
               try:<br>
                   ta_from = botslib.OldTransaction(row['idta'])<br>
                   ta_to = ta_from.copyta(status=EXTERNOUT)<br>
                   tofilename = self.filename_formatter(filename_mask,ta_from)<br>
                   if self.channeldict['ftpbinary']:<br>
                       fromfile = botslib.opendata(row['filename'], 'rb')<br>
                       self.session.storbinary(mode + tofilename, fromfile)<br>
                   else:<br>
                       fromfile = botslib.opendata(row['filename'], 'r')<br>
                       self.session.storlines(mode + tofilename, fromfile)<br>
                   fromfile.close()<br>
               except:<br>
                   txt = botslib.txtexc()<br>
                   ta_to.update(statust=ERROR,errortext=txt,filename='ftp:/'+posixpath.join(self.dirpath,tofilename),numberofresends=row['numberofresends']+1)<br>
               else:<br>
                   ta_to.update(statust=DONE,filename='ftp:/'+posixpath.join(self.dirpath,tofilename),numberofresends=row['numberofresends']+1)<br>
               finally:<br>
                   ta_from.update(statust=DONE)<br>
   </code></pre>

   <h4>

Example 3

.. raw:: html

   </h4>

In this case communication-type of the channel is 'ftp' or 'sftp'. The
class 'ftp' subclasses the standard 'ftp' method of bots. The
'disconnect' method of the ftp class is taken over with this
implementation. The bots channel should be configured to upload either
to a 'tmp' sub-directory, or with a '.tmp' extension. This function
renames the files once uploads are complete, this preventing the
recipient from processing partial files.

.. raw:: html

   <pre><code>'''<br>
   For safety when uploading to ftp servers, it is a good idea to rename/move<br>
   files once complete. This prevents the receiver processing partial files.<br>
   When all files have been sent and before the session is disconnected, the<br>
   files are renamed so the receiver can process them.<br>
   <br>
   Two methods are available:<br>
    1. Append extension ".tmp" to the channel filename<br>
       This method is simpler, but the receiver may still process the<br>
       .tmp files if it does not look for specific extensions to process.<br>
    2. Append subdirectory "/tmp" to the channel path<br>
       This requires an extra directory created on the server, you may not<br>
       be authorised to do this.<br>
   <br>
   Subclassing of ftp.disconnect. Import this to your communicationscript (ftp or sftp as required):<br>
       from _ftp_rename import ftp<br>
       from _ftp_rename import sftp<br>
   <br>
   Mike Griffin  4/09/2013<br>
   <br>
   '''<br>
   <br>
   import bots.communication as communication<br>
   import bots.botslib as botslib<br>
   import bots.botsglobal as botsglobal<br>
   <br>
   class ftp(communication.ftp):<br>
       def disconnect(self,*args,**kwargs):<br>
   <br>
           # rename files to remove .tmp extensions<br>
           if self.channeldict['filename'].endswith('.tmp'):<br>
               for f in self.session.nlst():<br>
                   if f.endswith('.tmp'):<br>
                       try:<br>
                           self.session.rename(f,f[:-4])<br>
                       except:<br>
                           pass<br>
   <br>
           # rename files from tmp subdirectory to parent directory<br>
           if self.channeldict['path'].endswith('/tmp'):<br>
               for f in self.session.nlst():<br>
                   try:<br>
                       self.session.rename(f,'../%s' %f)<br>
                   except:<br>
                       pass<br>
   <br>
           try:<br>
               self.session.quit()<br>
           except:<br>
               self.session.close()<br>
           botslib.settimeout(botsglobal.ini.getint('settings','globaltimeout',10))<br>
   <br>
   class sftp(communication.sftp):<br>
       def disconnect(self,*args,**kwargs):<br>
   <br>
           # rename files to remove .tmp extensions<br>
           if self.channeldict['filename'].endswith('.tmp'):<br>
               for f in self.session.listdir('.'):<br>
                   if f.endswith('.tmp'):<br>
                       try:<br>
                           self.session.rename(f,f[:-4])<br>
                       except:<br>
                           pass<br>
   <br>
           # rename files from tmp subdirectory to parent directory<br>
           if self.channeldict['path'].endswith('/tmp'):<br>
               for f in self.session.listdir('.'):<br>
                   try:<br>
                       self.session.rename(f,'../%s' %f)<br>
                   except:<br>
                       pass<br>
   <br>
           self.session.close()<br>
           self.transport.close()<br>
   </code></pre>

   <h4>

Example 4

.. raw:: html

   </h4>

In this case communication-type of the channel is 'ftp'. The class 'ftp'
subclasses the standard 'ftp' method of bots. The 'disconnect' method of
the ftp class is taken over with this implementation. This provides a
way to submit a remote command to the ftp server, for example to run a
program on that server. The bots channel is configured with the command
in the 'parameters' field.

.. raw:: html

   <pre><code>'''<br>
   Before disconnecting, send a remote command<br>
   Channel "parameters" holds the command to send<br>
   <br>
   Subclassing of ftp.disconnect. Import this to your communicationscript:<br>
       from _ftp_remote_command import ftp<br>
   <br>
   Mike Griffin  13/09/2013<br>
   '''<br>
   <br>
   import bots.communication as communication<br>
   import bots.botsglobal as botsglobal<br>
   <br>
   class ftp(communication.ftp):<br>
       def disconnect(self,*args,**kwargs):<br>
   <br>
           # send remote command to ftp server<br>
           botsglobal.logger.info('Send remote command: %s',self.channeldict['parameters'])<br>
           self.session.sendcmd('RCMD %s' %self.channeldict['parameters'])<br>
   <br>
           try:<br>
               self.session.quit()<br>
           except:<br>
               self.session.close()<br>
           botslib.settimeout(botsglobal.ini.getint('settings','globaltimeout',10))<br>
   </code></pre>

