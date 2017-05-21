## Installation FAQ

-   I try to install bots at Windows Vista/7, but.....
    -   Probably a rights problem - you'll have to have administrator rights in order to do a proper install.
    -   Right click the installer program, and choose 'Run as Administrator'.
    -   Bots works on Vista/7/8!
    -   sometimes the shortcut is not installed in the menu, and you will have to make this manually. See [StartGetBotsRunning](StartGetBotsRunning.md)
-   Does bots have edifact and x12 messages installed out-of-the-box?
    -   No. But this can be downloaded on the [sourceforge site](https://sourceforge.net/projects/bots/files) either as part of a working configuration (plugin) of separate (grammars).
-   Bots is not working on linux - rights problems.
    -   Start bots-webserver and bots-engine with sufficient rights - e.g. as root.
    -   Change the owner/rights of the files in botssys, usersys and config; run bots-webserver/bots-engine without root rights.
-   During windows installation: Error:

```
close failed in file object destructor: 
sys.excepthook is missing 
lost sys.stderr
```
    -   seems to happen when UAC is turned off.
    -   Actually bots just seems to be installed OK, and works OK.....
    -   Fixed this in version 3.2