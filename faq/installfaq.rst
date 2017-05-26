Installation FAQ
----------------

**I try to install bots at Windows 7/10, but.....**
    * Probably a rights problem - you'll have to have administrator rights in order to do a proper install.
    * Right click the installer program, and choose 'Run as Administrator'.
    * sometimes the shortcut is not installed in the menu, and you will have to make this manually.
    
**Does bots have edifact and x12 messages installed out-of-the-box?**
    No. But this can be downloaded on the sourceforge site either as part of a working configuration (plugin) of separate (grammars).
    
**Bots is not working on linux - rights problems.**
    Did you start bots-webserver and/or bots-engine with sufficient rights - e.g. as root.
    Change the owner/rights of the files in botssys, usersys and config; run bots-webserver/bots-engine without root rights.
    
**Error during windows installation**

    .. code-block:: console 

        close failed in file object destructor:
        sys.excepthook is missing
        lost sys.stderr

    * seems to happen when UAC is turned off.
    * Actually bots just seems to be installed OK, and works OK.....
    * Fixed this in version 3.2
