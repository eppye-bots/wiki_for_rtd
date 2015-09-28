communication type 'communicationscript'
----------------------------------------

In this case, the channel must be configured with Type:
communicationscript. In the communicationscript some functions will be
called:

.. raw:: html

   <ul><li>

connect (required)

.. raw:: html

   </li><li>

main (optional, 'main' should handle files one by one)

.. raw:: html

   </li><li>

disconnect (optional)

.. raw:: html

   </li></ul>

Different ways of working:

.. raw:: html

   <ol><li>

for incoming files (bots receives the files):

.. raw:: html

   <ul><li>

connect puts all files in a directory, there is no 'main' function. bots
can remove the files (if you use the 'remove' switch of the channel).
See example 1.

.. raw:: html

   </li><li>

connect only builds the connection, 'main' is a generator that passes
the messages one by one (using 'yield'). bots can remove the files (if
you use the 'remove' switch of the channel). See example 2.

.. raw:: html

   </li></ul></li><li>

for outgoing files (bots sends the files):

.. raw:: html

   <ul><li>

no 'main' function: the processing of all the files can be done in
'disconnect'. bots can remove the files (if you use the 'remove' switch
of the channel). See example 3.

.. raw:: html

   </li><li>

if there is a 'main' function: the 'main' function is called by bots
after writing each file. bots can remove the files (if you use the
'remove' switch of the channel). See example 4.

.. raw:: html

   </li></ul></li></ol>

.. raw:: html

   <h3>

Example 1: incoming files via external program all at once

.. raw:: html

   </h3>

Calls an external program. Think eg of a specific communication module
for a VAN. All files are received at once to a folder, then processed
like a normal file channel.

.. raw:: html

   <pre><code>import subprocess<br>
   <br>
   def connect(channeldict,*args,**kwargs):<br>
       subprocess.call(['C:/Program files/my VAN/comms-module.exe','-receive'])<br>
   </code></pre>

.. raw:: html

   <h3>

Example 2: incoming files via external program one by one

.. raw:: html

   </h3>

TODO: make a valid example using yield. main is a generator.

.. raw:: html

   <pre><code>import subprocess<br>
   <br>
   def connect(channeldict,*args,**kwargs):<br>
       ''' function does nothing but it is required.'''<br>
       pass<br>
   <br>
   def main(channeldict,*args,**kwargs):<br>
   <br>
       yield ?<br>
   <br>
   </code></pre>

.. raw:: html

   <h3>

Example 3: outgoing files via external program all at once

.. raw:: html

   </h3>

Calls an external program. Think eg of a specific communication module
for a VAN. In this example the 'disconnect' script is called after all
files are written to directory; in disconnect all files are passed to
external communication-module.

.. raw:: html

   <pre><code>import subprocess<br>
   import os<br>
   <br>
   def connect(channeldict,*args,**kwargs):<br>
       ''' function does nothing but it is required.'''<br>
       pass<br>
   <br>
   def disconnect(channeldict,*args,**kwargs):<br>
       subprocess.call(['C:/Program files/my VAN/comms-module.exe','-send',os.path.join(channeldict['path'],'*.xml'])<br>
   </code></pre>

.. raw:: html

   <h3>

Example 4: outgoing files via external program one by one

.. raw:: html

   </h3>

Calls an external program. Think eg of a specific communication module
for a VAN. In this example the 'main' script is called for each outgoing
file.

.. raw:: html

   <pre><code>import subprocess<br>
   <br>
   def connect(channeldict,*args,**kwargs):<br>
       ''' function does nothing but it is required.'''<br>
       pass<br>
   <br>
   def main(channeldict,filename,ta,*args,**kwargs):<br>
       subprocess.call(['C:/Program files/my VAN/comms-module.exe','-send',filename])<br>
   </code></pre>

.. raw:: html

   <h3>

Example 5: outgoing files to a printer

.. raw:: html

   </h3>

Send data (eg. ZPL code to print fancy labels) directly to a Windows
configured printer. The printer can be defined in Windows either as
"Generic/Text Only" or with the proper driver, because this script just
sends raw data, bypassing the driver. Dependencies: Requires pywin32
Reference: http://timgolden.me.uk/pywin32-docs/win32print.html

.. raw:: html

   <pre><code>import os<br>
   import win32print<br>
   import bots.transform as transform<br>
   <br>
   def connect(channeldict,*args,**kwargs):<br>
       ''' function does nothing but it is required.'''<br>
       pass<br>
   <br>
   def main(channeldict,filename,ta,*args,**kwargs):<br>
   <br>
       # set printer values required<br>
       ta.synall()<br>
       printer = transform.partnerlookup(ta.topartner,'attr1')<br>
       jobname = ta.botskey<br>
   <br>
       # read the output file<br>
       with open(filename,'r') as content_file:<br>
           content = content_file.read()<br>
   <br>
       # send data to the printer<br>
       hPrinter = win32print.OpenPrinter(printer)<br>
       hJob = win32print.StartDocPrinter(hPrinter,1,(jobname,None,'RAW'))<br>
       win32print.WritePrinter(hPrinter,content)<br>
       win32print.EndDocPrinter(hPrinter)<br>
       win32print.ClosePrinter(hPrinter)<br>
   </code></pre>

