General FAQ
-----------

**Files are 'stuck'**
    Basically bots expects input to lead to output. When a file is 'stuck' input did not lead to output.
    Somehow the setup you made is not OK. Files go in, but nothing comes out.
    Often this is the problem: Have you put any :doc:`filtering <../configuration/route/composite-routes>` on the output of your route? (under 'Filtering for outchannel' in the route configuration).
    Filtering allows you send only particular files via an out-channel; but a file that does not match one of the filters will end up "stuck" because Bots does not know where to send it. 
    If you have only one outchannel, there is no need for filtering.

**Incoming edi-files are read over and over again**
    In the in-channel, there is a 'remove'-option. 
    Turn it on to have incoming files removed after reading. 
    The 'not-remove' option is mostly used in development.

**Incoming files can be seen but are not picked up by Bots (particularly with unc paths)**
    This is usually a permission problem. 
    Remember that if you are running Bots Engine as a daemon/service it may be running under a system user account. 
    Make sure the user has rights to the folder/files, or run the engine with a special user account that does have the required rights. 
    It is best to use the :ref:`jobqueue server <job-queue-server>` so that engine runs started from the GUI also run under the special user account.

**Error in Internet Explorer: 'ValueError: invalid literal for int() with base 10'**
    This has to do with the compatibility-settings of IE (tools->compatibility view settings). 
    Text from Microsoft: 'Websites that were designed for earlier versions of Internet Explorer might not display correctly in IE8, IE9, or IE10. 
    When you turn on Compatibility View, the webpage you're viewing, as well as any other webpages within the website's domain, will be displayed as if you were using an earlier version of Internet Explorer. 
    So if the compatibility view is used this error occurs, else it goes OK.'

**Error in Internet Explorer: 'DoesNotExist?: report matching query does not exist.'**
    Same problem as last question: compatibility-settings of IE (tools->compatibility view settings). 

**"root" of incoming message is empty; either split messages or use inn.getloop**
    This may occur with incoming files that have only one record format. 
    Even if the whole file is one edi message, you need to use :doc:`nextmessageblock <../configuration/grammars/nextmessageblock>` in your incoming grammar.

**Outgoing files to sftp server result in 'IOError: [Errno 13] Requested operation is not supported.'**
    Error occurs during out-communication via FTP. 
    Some FTP-servers do no support 'APPE' command (only 'STOR'). 
    To resolve add '{overwrite}' to filename, eg: ``{overwrite}OUT_{datetime:%Y%m%d%H%M%S}_*.edi``.
    Please make sure that filename is always unique by using ``*``.

**error_perm: 502 Command not implemented.**
    Error occurs during out-communication via FTP. 
    Some FTP-servers do no support 'APPE' command (only 'STOR'). 
    To resolve add '{overwrite}' to filename, eg: ``{overwrite}OUT_{datetime:%Y%m%d%H%M%S}_*.edi``.
    Please make sure that filename is always unique by using ``*``.

    Another option is to set the 'FTP active mode' in channel (under FTP specfic).

**ftp server gives a timeout when writing file (connect is OK)**
    In channel, set the 'FTP active mode' (under FTP specfic).
