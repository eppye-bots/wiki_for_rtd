## communication type 'communicationscript' 

In this case, the channel must be configured with Type: communicationscript.  
In the communicationscript some functions will be called:

-   connect (required)
-   main (optional, 'main' should handle files one by one)
-   disconnect (optional)

Different ways of working:

1.  for incoming files (bots receives the files):
    -   connect puts all files in a directory, there is no 'main'
        function. bots can remove the files (if you use the 'remove'
        switch of the channel). See example 1.
    -   connect only builds the connection, 'main' is a generator that
        passes the messages one by one (using 'yield'). bots can remove
        the files (if you use the 'remove' switch of the channel). See
        example 2.

2.  for outgoing files (bots sends the files):
    -   no 'main' function: the processing of all the files can be done
        in 'disconnect'. bots can remove the files (if you use the
        'remove' switch of the channel). See example 3.
    -   if there is a 'main' function: the 'main' function is called by
        bots after writing each file. bots can remove the files (if you
        use the 'remove' switch of the channel). See example 4.


### Example 1: incoming files via external program all at once

Calls an external program.  
Think eg of a specific communication module for a VAN.  
All files are received at once to a folder, then processed like a
normal file channel. 


    import subprocess

    def connect(channeldict,*args,**kwargs):
        subprocess.call(['C:/Program files/my VAN/comms-module.exe','-receive'])


### Example 2: incoming files via external program one by one

TODO: make a valid example using yield.  
main is a generator.

    import subprocess

    def connect(channeldict,*args,**kwargs):
        ''' function does nothing but it is required.'''
        pass

    def main(channeldict,*args,**kwargs):

        yield ?


### Example 3: outgoing files via external program all at once

Calls an external program.  
Think eg of a specific communication module for a VAN.  
In this example the 'disconnect' script is called after all files are
written to directory;  
in disconnect all files are passed to external communication-module.

    import subprocess
    import os

    def connect(channeldict,*args,**kwargs):
        ''' function does nothing but it is required.'''
        pass

    def disconnect(channeldict,*args,**kwargs):
        subprocess.call(['C:/Program files/my VAN/comms-module.exe','-send',os.path.join(channeldict['path'],'*.xml'])


### Example 4: outgoing files via external program one by one

Calls an external program.  
Think eg of a specific communication module for a VAN.  
In this example the 'main' script is called for each outgoing file.

    import subprocess

    def connect(channeldict,*args,**kwargs):
        ''' function does nothing but it is required.'''
        pass

    def main(channeldict,filename,ta,*args,**kwargs):
        subprocess.call(['C:/Program files/my VAN/comms-module.exe','-send',filename])


### Example 5: outgoing files to a printer

Send data (eg. ZPL code to print fancy labels) directly to a Windows
configured printer.  
The printer can be defined in Windows either as "Generic/Text Only" or
with the proper driver, because this script just sends raw data, bypassing the
driver.  
Dependencies: Requires pywin32  
Reference: <http://timgolden.me.uk/pywin32-docs/win32print.html>

    import os
    import win32print
    import bots.transform as transform

    def connect(channeldict,*args,**kwargs):
        ''' function does nothing but it is required.'''
        pass

    def main(channeldict,filename,ta,*args,**kwargs):

        # set printer values required
        ta.synall()
        printer = transform.partnerlookup(ta.topartner,'attr1')
        jobname = ta.botskey

        # read the output file
        with open(filename,'r') as content_file:
            content = content_file.read()

        # send data to the printer
        hPrinter = win32print.OpenPrinter(printer)
        hJob = win32print.StartDocPrinter(hPrinter,1,(jobname,None,'RAW'))
        win32print.WritePrinter(hPrinter,content)
        win32print.EndDocPrinter(hPrinter)
        win32print.ClosePrinter(hPrinter)
