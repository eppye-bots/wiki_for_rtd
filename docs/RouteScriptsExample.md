## Preprocessing and Postprocessing examples

Some recipes for preprocessing edi files.  
Plugin 'demo\_preprocessing' at [the bots sourceforge
site](http://sourceforge.net/projects/bots/files/plugins/) demonstrates
preprocessing.


### Example 1: Discard input files that are too small


    import os
    import bots.preprocess as preprocess
    from bots.botsconfig import *

    def postincommunication(routedict,*args,**kwargs):
        ''' function is called after the communication in the route.'''
        preprocess.preprocess(routedict=routedict,function=discard_file)

    def discard_file(ta_from,endstatus,*args,**kwargs):
        ''' discard files that are to small (zero files)''' 
        ta_from.synall()
        filesize = ta_from.filesize
        if filesize < 100:    #filesize in bytes
            ta_from.update(statust=DONE)                       #statust=DONE: bots discards file, gives no errors.
        else:
            ta_to = ta_from.copyta(status=endstatus)           #make new transaction for bots database
            ta_to.update(statust=OK,filename=ta_from.filename) #update outmessage transaction (same) filename



### Example 2: Extract data from PDF file (to csv)

    # Extract data from PDF file (to csv)
    # x_group: group text closer than this as one field (default 10)
    # y_group: group lines closer than this as one line (default 5)
    # password: if required

    import bots.preprocess as preprocess

    def postincommunication(routedict,*args,**kwargs):
        preprocess.preprocess(routedict,preprocess.extractpdf,x_group=12,y_group=3,password='secret')


### Example 3: Manipulate records without BOTSID

    import bots.preprocess as preprocess
    import bots.botslib as botslib
    import bots.botsglobal as botsglobal
    from bots.botsconfig import *

    def postincommunication(routedict,*args,**kwargs):
        preprocess.preprocess(routedict,custom_preprocess)

    def custom_preprocess(ta_from,endstatus,*args,**kwargs):
        try:
            # copy ta for preprocessing
            ta_to = ta_from.copyta(status=endstatus)

            # open the files
            infile = botslib.opendata(ta_from.filename,'r')
            tofile = botslib.opendata(str(ta_to.idta),'wb')

            # preprocessing: read infile, write tofile
            # This file has headers and lines, but no field that can be used for BOTSID!
            # Determine the line type from the data, and add HDR or LIN in first column
            # Text heading lines and blank lines are omitted
            for line in infile:
                if '\tAU' in line: 
                    tofile.write('HDR\t' + line)
                elif ('\tWAIT' in line or
                      '\tFULL' in line or
                      '\tEMPTY' in line):
                    tofile.write('LIN\t' + line)

            infile.close()
            tofile.close()

            ta_to.update(statust=OK,filename=str(ta_to.idta)) #update outmessage transaction with ta_info; 
        except:
            txt=botslib.txtexc()
            botsglobal.logger.error(u'Custom preprocess failed. Error:\n%s',txt)
            raise botslib.InMessageError(u'Custom preprocess failed. Error:\n$error',error=txt)



### Example 4: Sort input file

    import bots.preprocess as preprocess
    import bots.botslib as botslib
    import bots.botsglobal as botsglobal
    from bots.botsconfig import *

    def postincommunication(routedict,*args,**kwargs):
        preprocess.preprocess(routedict,sort_file)

    def sort_file(ta_from,endstatus,*args,**kwargs):
        try:
            # copy ta for preprocessing
            ta_to = ta_from.copyta(status=endstatus)

            # open the files
            infile = botslib.opendata(ta_from.filename,'r')
            tofile = botslib.opendata(str(ta_to.idta),'wb')

            # sort output
            lines = infile.readlines()
            lines.sort()
            for line in lines:
                tofile.write(line)

            infile.close()
            tofile.close()

            ta_to.update(statust=OK,filename=str(ta_to.idta)) #update outmessage transaction with ta_info; 
        except:
            txt=botslib.txtexc()
            botsglobal.logger.error(u'Sort preprocess failed. Error:\n%s',txt)
            raise botslib.InMessageError(u'Sort preprocess failed. Error:\n$error',error=txt)


### Example 5: Postprocessing

Post processing works the same way as pre processing, except it is done
before out communication.

    import bots.preprocess as preprocess
    import bots.botslib as botslib
    import bots.botsglobal as botsglobal
    from bots.botsconfig import *

    def preoutcommunication(routedict,*args,**kwargs):
        preprocess.postprocess(routedict,split_lines)

    def split_lines(ta_from,endstatus,,*args,**kwargs):
        try:
            # copy ta for postprocessing, open the files
            ta_to = ta_from.copyta(status=endstatus)
            infile = botslib.opendata(ta_from.filename,'r')
            tofile = botslib.opendata(str(ta_to.idta),'wb')

            # split every line at the first separator (space)
            # output the two parts on separate lines
            for line in infile:
                part = line.partition(' ')
                tofile.write(part[0] + '\n' + part[2])

            # close files and update outmessage transaction with ta_info
            infile.close()
            tofile.close()
            ta_to.update(statust=OK,filename=str(ta_to.idta))

        except:
            txt=botslib.txtexc()
            botsglobal.logger.error(_(u'split_lines postprocess failed. Error:\n%s'),txt)
            raise botslib.OutMessageError(_(u'split_lines postprocess failed. Error:\n$error'),error=txt)


### Example 6: Preprocessing an encrypted file

This example uses gnupg to decrypt a file before processing it in Bots.

    import bots.preprocess as preprocess
    import bots.botslib as botslib
    import gnupg

    # Preprocessing - Decrypt infile using GPG
    # Dependencies: python-gnupg-0.3.0
    #   botssys/gnugpghome directory, containing:
    #     gpg binary files (gpg.exe and iconv.dll)
    #     keys (pubring.gpg, secring.gpg, trustdb.gpg)
    #     passphrase.txt

    def postincommunication(routedict,*args,**kwargs):
        # preprocess to decrypt, then passthrough (no translation)
        preprocess.preprocess(routedict,decrypt_GPG)
        transform.addinfo(change={'status':MERGED},where={'status':FILEIN,'idroute':routedict['idroute']})

    def decrypt_GPG(ta_from,endstatus,*args,**kwargs):

        # copy ta for preprocessing
        ta_to = ta_from.copyta(status=endstatus)

        # gnupghome contains the gpg binary files, public/private keys, and passphrase
        gnupghome = botslib.join(botsglobal.ini.get('directories','botssys'),'gnupghome')
        passphrase = open(botslib.join(gnupghome,'passphrase.txt'),'r').read()
        gpgbinary = botslib.join(gnupghome,'gpg.exe')

        # Here is where we do the actual decryption
        gpg = gnupg.GPG(gnupghome=gnupghome,gpgbinary=gpgbinary)
        with botslib.opendata(ta_from.filename,'rb') as input:
            status = gpg.decrypt_file(input, passphrase=passphrase,output=botslib.abspathdata(str(ta_to.idta)))

        # log the results and finish
        botsglobal.logger.debug(status.stderr)
        if status.ok:
            botsglobal.logger.info(status.status)
            ta_to.update(statust=OK,filename=str(ta_to.idta))
        else:
            botsglobal.logger.error(status.status)
            ta_to.update(statust=ERROR,filename=str(ta_to.idta))
            raise PreprocessError(status.status + '\n' + status.stderr)

    class PreprocessError(botslib.BotsError):
        pass


### Example 7: Preprocessing to ignore/remove XML namespaces

This example changes the default namespace to a namespace prefix (so it
is ignored). It also removes a namespace prefix (ENV). You may need to
use either or both of these methods, depending on the content of your
XML file.

    #-------------------------------------------------------------------------------
    # preprocess - Remove XML namespaces to simplify grammar and mapping
    # Generally Bots does not need to use the xmlns for incoming files
    # This example handles both default and prefix namespaces

    def postincommunication(routedict):

        def _preprocess(ta_from,endstatus,**argv):

            # copy ta for preprocessing
            ta_to = ta_from.copyta(status=endstatus)

            # open the files
            infile = botslib.opendata(ta_from.filename,'r')
            tofile = botslib.opendata(str(ta_to.idta),'wb')

            for line in infile:
                tofile.write(line.replace('xmlns=','xmlns:NOTUSED=').replace('<ENV:','<').replace('</ENV:','</'))

            # close files and update outmessage transaction
            infile.close()
            tofile.close()
            ta_to.update(statust=OK,filename=str(ta_to.idta))

        preprocess.preprocess(routedict,_preprocess)
