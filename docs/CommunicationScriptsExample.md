## Examples for small user exit

#### Filter email attachments

Some edi-partners send signatures etc in their email. Script does a
simple check if incoming attachment starts with 'UNB'. (Note: Bots
treats any text in the email body as another "attachment")

    def accept_incoming_attachment(channeldict,ta,charset,content,contenttype,*args,**kwargs):
        if 'UNB' in content[0:50]:
            return True   #attachments is OK
        else:
            return False  #skip this attachment


#### Set email subject

Some edi-partners send signatures etc in their email.  
By default bots uses a number for emails.  
Sometimes you want a more meaningfull subject.

    def subject(channeldict,ta,subjectstring,content,*args,**kwargs):
        ta.synall()        #needed to get access to attributes of object ta (eg ta.frompartner)
        return 'EDI messages from ' + ta.frompartner + '_' + subjectstring



#### Name archive file same as input file

Not needed for bots 3.**; do this via setting in bots.ini
**

    import os
    import bots.botslib as botslib

    def archivename(channeldict,idta,filename,*args,**kwargs):
         taparent=botslib.OldTransaction(idta=idta)
         ta_list = botslib.trace_origin(ta=taparent,where={'status':EXTERNIN})
         archivename = os.path.basename(ta_list[0].filename)
         return archivename 


#### Set the archive path

Path root is set in channel.  
Add sub-dir per date, then sub-dir per channel under it.

    import time
    import bots.botslib as botslib

    def archivepath(channeldict,*args,**kwargs):
        archivepath = botslib.join(channeldict['archivepath'],time.strftime('%Y%m%d'),channeldict['idchannel'])
        return archivepath


#### Partners in the output file name

Not needed for bots 3.**; do this via file name in GUI**

    def filename(channeldict,filename,ta,*args,**kwargs):
        ta.synall()        #needed to get access to attributes of object ta (eg ta.frompartner)
        return ta.frompartner + '_' + ta.topartner + '_' + filename


#### Name the output file from botskey

botskey can be set in grammar or mapping, eg. from customer's order
number.  
If no botskey is found, the default file naming method will be used.  
Syntax must contain 'merge':False.  
Not needed for bots 3.**; do this via file name in GUI.**

    def filename(channeldict,filename,ta,*args,**kwargs):
        ta.synall()
        if ta.botskey:
            return filename + ta.botskey
        else:
            return filename


#### Name the output file same as input file

Syntax must contain 'merge':False.  
Not needed for bots 3.

