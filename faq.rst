.. |br| raw:: html

   <br />

FAQ
====

Installation
------------

When starting bots-webserver the window disappears after a few seconds?
    Start the bots-webserver from the command line; you will be able to see what goes wrong. 
    (Windows, python 2.7) go to command line and: `` c:\python27\python c:\python27\Scripts\bots-webserver.py``
    For the most common cause for the problem see the next question.

Bots-webserver gives error: IOError: Port 8080 not free on 'x.x.x.x' (or similar).
    *   Another program already uses this 'port'.
    *   Adapt the port bots uses: in configuration file ``bots/config/bots.ini`` look for 'port'.
    *   Change port to eg 8090
    *   Start bots-webserver again.
    *   In your browser you will have to indicate another port eg: ``http://localhost:8090``

I try to install bots at Windows Vista/7, but.....
    *   Probably a rights problem - you'll have to have administrator rights in order to do a proper install.
    *   Right click the installer program, and choose 'Run as Administrator'.
    *   Sometimes the shortcut is not installed in the menu, and you will have to make this manually. See `StartGetBotsRunning <StartGetBotsRunning.md>`__

Bots is not working on linux - rights problems.
    Either:
    #.   Start bots-webserver and bots-engine with sufficient rights - e.g. as root.
    #.   Change the owner/rights of the files in botssys, usersys and config; run bots-webserver/bots-engine without root rights.

During windows installation: Error:

   ::

       close failed in file object destructor: 
       sys.excepthook is missing 
       lost sys.stderr

   *    seems to happen when UAC is turned off.
   *    Actually bots just seems to be installed OK, and works OK.....



Troubleshoot
------------

Files get "stuck" 
    Basically bots expects input to lead to
    output. When a file is 'stuck' input did not lead to output. 

    Somehow the setup you made is not OK. Files go in, but nothing comes
    out. Often this is the problem: Have you put any filtering on the output
    of your route? (under 'Filtering for outchannel' in the route
    configuration). Filtering allows you send only particular files via an
    out-channel; but a file that does not match one of the filters will end
    up "stuck" because Bots does not know where to send it. If you have only
    one outchannel, there is no need for filtering. 

Incoming edi-files are read over and over again 
    In the in-channel, there is a
    'remove'-option. Turn it on to have incoming files removed after
    reading. (it is more normal to have this on, but turning it off is handy
    in development). 

Outgoing files to sftp server result in "IOError:[Errno 13] Requested operation is not supported." 
    It appears
    that some sftp severs do not support append mode (bots default mode). In
    this case include {overwrite} in the channel filename specification to
    force write mode. See here for output filename formatting. 

Incoming files can be seen but are not picked up by Bots (particularly with unc paths) 
    This is usually a permission problem. Remember that if
    you are running Bots Engine as a daemon/service it may be running under
    a system user account. Make sure the user has rights to the
    folder/files, or run the engine with a special user account that does
    have the required rights. It is best to use the Jobqueue so that engine
    runs started from the GUI also run under the special user account. 

Error in Internet Explorer: ValueError: invalid literal for int() with base 10
    This has to do with the compatibility-settings of IE
    (tools->compatibility view settings). Text from Microsoft: Websites that
    were designed for earlier versions of Internet Explorer might not
    display correctly in IE8, IE9, or IE10. When you turn on Compatibility
    View, the webpage you're viewing, as well as any other webpages within
    the website's domain, will be displayed as if you were using an earlier
    version of Internet Explorer. So: if the compatibility view is used this
    error occurs, else it goes OK. Solution: do not this the compatibility
    view in IE, or use another browser. 

Error in Internet Explorer: DoesNotExist: report matching query does not exist. 
    Same problem
    as last question: This has to do with the compatibility-settings of IE
    (tools->compatibility view settings). Text from Microsoft: Websites that
    were designed for earlier versions of Internet Explorer might not
    display correctly in IE8, IE9, or IE10. When you turn on Compatibility
    View, the webpage you're viewing, as well as any other webpages within
    the website's domain, will be displayed as if you were using an earlier
    version of Internet Explorer. So: if the compatibility view is used this
    error occurs, else it goes OK. Solution: do not this the compatibility
    view in IE, or use another browser. 

"root" of incoming message is empty; either split messages or use inn.getloop 
    This may occur with
    incoming files that have only one record format. Even if the whole file
    is one edi message, you need to use nextmessageblock in your incoming
    grammar. 

error_perm: 502 Command not implemented. 
    Answer1: Some FTP-servers do no support 'APPE' command (only 'STOR'). In filename use: ``{overwrite}``. Eg: |br|  
    ``OUT\_{messagetype}\ *{datetime:%Y%m%d%H%M%S}{overwrite}.edi``
     |br| Note that this {overwrite} thing only takes care of using STOR instead of APPE. Make sure filename is unique (use *\  !).  |br| 
    Answer2: Error occurs in communication via FTP. In channel, set the 'FTP active mode' (under FTP specfic).

ftp server gives a timeout when writing file (connect is OK) 
    Answer1: In channel, set the 'FTP active mode' (under FTP specfic).



General
-------

Does bots have edifact and x12 messages installed out-of-the-box?
    No. But this can be downloaded on the `sourceforge site <https://sourceforge.net/projects/bots/files>`__ either as
    part of a working configuration (plugin) of separate (grammars).

Can I run multiple instances of bots-engine in parallel?
    No, this is not possible. Instead use bots jobqueue-server for better control of running the engine.

