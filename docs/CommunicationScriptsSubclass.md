## Subclassing communication

It is possible to overwrite bots communication methods completely.  
This is done using python subclassing.  
Again, as with all communication scripting there should be a file in
usersys/communicationscripts with the same name as the channel (and
extension '.py')

#### Example 1

In this case communication-type of the channel is 'file'. Bots will
check the communication-script file if there is a class called 'file'
and use that.
 The class 'file' subclasses the standard 'file' method of bots.

    import bots.communication as communication

    class file(communication.file):
        def connect(self,*args,**kwargs):
            #do the preparing work
            print 'in connect method'

#### Example 2

In this case communication-type of the channel is 'ftp'.
 The class 'ftp' subclasses the standard 'ftp' method of bots. The
'outcommunicate' method of the ftp class is taken over with this
implementation.

    import bots.communication as communication
    import bots.botslib as botslib
    from bots.botsconfig import *

    class ftp(communication.ftp):
        @botslib.log_session
        def outcommunicate(self,*args,**kwargs):
            #get right filename_mask & determine if fixed name (append) or files with unique names
            filename_mask = self.channeldict['filename'] if self.channeldict['filename'] else '*'
            if '{overwrite}' in filename_mask:
                filename_mask = filename_mask.replace('{overwrite}','')
                mode = 'STOR '
            else:
                mode = 'APPE '
            for row in botslib.query('''SELECT idta,filename,numberofresends
                                        FROM ta
                                        WHERE idta>%(rootidta)s
                                          AND status=%(status)s
                                          AND statust=%(statust)s
                                          AND tochannel=%(tochannel)s
                                            ''',
                                        {'tochannel':self.channeldict['idchannel'],'rootidta':self.rootidta,
                                        'status':FILEOUT,'statust':OK}):
                try:
                    ta_from = botslib.OldTransaction(row['idta'])
                    ta_to = ta_from.copyta(status=EXTERNOUT)
                    tofilename = self.filename_formatter(filename_mask,ta_from)
                    if self.channeldict['ftpbinary']:
                        fromfile = botslib.opendata(row['filename'], 'rb')
                        self.session.storbinary(mode + tofilename, fromfile)
                    else:
                        fromfile = botslib.opendata(row['filename'], 'r')
                        self.session.storlines(mode + tofilename, fromfile)
                    fromfile.close()
                except:
                    txt = botslib.txtexc()
                    ta_to.update(statust=ERROR,errortext=txt,filename='ftp:/'+posixpath.join(self.dirpath,tofilename),numberofresends=row['numberofresends']+1)
                else:
                    ta_to.update(statust=DONE,filename='ftp:/'+posixpath.join(self.dirpath,tofilename),numberofresends=row['numberofresends']+1)
                finally:
                    ta_from.update(statust=DONE)

#### Example 3

In this case communication-type of the channel is 'ftp' or 'sftp'.  
The class 'ftp' subclasses the standard 'ftp' method of bots. The
'disconnect' method of the ftp class is taken over with this
implementation. The bots channel should be configured to upload either
to a 'tmp' sub-directory, or with a '.tmp' extension. This function
renames the files once uploads are complete, this preventing the
recipient from processing partial files.

    '''
    For safety when uploading to ftp servers, it is a good idea to rename/move
    files once complete. This prevents the receiver processing partial files.
    When all files have been sent and before the session is disconnected, the
    files are renamed so the receiver can process them.

    Two methods are available:
     1. Append extension ".tmp" to the channel filename
        This method is simpler, but the receiver may still process the
        .tmp files if it does not look for specific extensions to process.
     2. Append subdirectory "/tmp" to the channel path
        This requires an extra directory created on the server, you may not
        be authorised to do this.

    Subclassing of ftp.disconnect. Import this to your communicationscript (ftp or sftp as required):
        from _ftp_rename import ftp
        from _ftp_rename import sftp

    Mike Griffin  4/09/2013

    '''

    import bots.communication as communication
    import bots.botslib as botslib
    import bots.botsglobal as botsglobal

    class ftp(communication.ftp):
        def disconnect(self,*args,**kwargs):

            # rename files to remove .tmp extensions
            if self.channeldict['filename'].endswith('.tmp'):
                for f in self.session.nlst():
                    if f.endswith('.tmp'):
                        try:
                            self.session.rename(f,f[:-4])
                        except:
                            pass

            # rename files from tmp subdirectory to parent directory
            if self.channeldict['path'].endswith('/tmp'):
                for f in self.session.nlst():
                    try:
                        self.session.rename(f,'../%s' %f)
                    except:
                        pass

            try:
                self.session.quit()
            except:
                self.session.close()
            botslib.settimeout(botsglobal.ini.getint('settings','globaltimeout',10))

    class sftp(communication.sftp):
        def disconnect(self,*args,**kwargs):

            # rename files to remove .tmp extensions
            if self.channeldict['filename'].endswith('.tmp'):
                for f in self.session.listdir('.'):
                    if f.endswith('.tmp'):
                        try:
                            self.session.rename(f,f[:-4])
                        except:
                            pass

            # rename files from tmp subdirectory to parent directory
            if self.channeldict['path'].endswith('/tmp'):
                for f in self.session.listdir('.'):
                    try:
                        self.session.rename(f,'../%s' %f)
                    except:
                        pass

            self.session.close()
            self.transport.close()

#### Example 4

In this case communication-type of the channel is 'ftp'.  
The class 'ftp' subclasses the standard 'ftp' method of bots. The
'disconnect' method of the ftp class is taken over with this
implementation. This provides a way to submit a remote command to the
ftp server, for example to run a program on that server. The bots
channel is configured with the command in the 'parameters' field.

    '''
    Before disconnecting, send a remote command
    Channel "parameters" holds the command to send

    Subclassing of ftp.disconnect. Import this to your communicationscript:
        from _ftp_remote_command import ftp

    Mike Griffin  13/09/2013
    '''

    import bots.communication as communication
    import bots.botsglobal as botsglobal

    class ftp(communication.ftp):
        def disconnect(self,*args,**kwargs):

            # send remote command to ftp server
            botsglobal.logger.info('Send remote command: %s',self.channeldict['parameters'])
            self.session.sendcmd('RCMD %s' %self.channeldict['parameters'])

            try:
                self.session.quit()
            except:
                self.session.close()
            botslib.settimeout(botsglobal.ini.getint('settings','globaltimeout',10))
