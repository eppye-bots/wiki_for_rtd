## Upgrade bots version 2.0.`*` -> 2.1.0 


### Procedure
1.  Use update plugin:
    -   Get the plugin at [sourceforge:](http://sourceforge.net/projects/bots/files/bots%20open%20source%20edi%20software/).
    -   Mind there are 2 version of the plugin, depending upon the version of django you use.
    -   Read like a normal plugin (bots-monitor->systasks->read plugin).
    -   Stop the web-server.
    -   Restart bots-webserver.

### Compatibility

Version 2.1.0 is upward compatible with previous versions in 2.`*`.`*`-series:

-   no data migration needed
-   grammars, translations etc mostly will work as before

### Compatibility notes ###

1.  After upgrading, some (eg. older edifact) grammars can give errors. This is due to stricter checking of grammars. 
    The records in a grammar are now checked for unique field-names: the same field name is not allowed in a record. 
    This was never OK, but was not checked). Typical error:

```
GrammarError: Grammar "...usersys/grammars/edifact.ORDERSD96AUNEAN008", record "FII": field "C078.3192" appears twice. Field names should be unique within a record. 
```

> The culprit is the file D96Arecords (or similar), the FII segment has an error in it.
    * Solution 1: adapt grammar manually; change FII segment:
```
 ['C078.3192','C',35,'A'],
 ['C078.3192','C',35,'A'],
```
> > to:
```
 ['C078.3192','C',35,'A'],
 ['C078.3192#2','C',35,'A'],
```
    * Solution 2: use plugin 'update\_edifact\_recorddefs.zip' (same directory as update-plugins. this plugin only contains edifact records for D93A and D96A).

### Changes in bots.ini

You can use your old bots.ini with no problem, reasonable defaults have been used. Following are the new options added.

```
[settings]

#adminlimit: number of lines displayed on one screen for configuration items; default is value of 'limit'
#adminlimit = 30

#for incoming channels: limit the time in-communication is done (in seconds). Default is 60. This is the global parameter, can also be limited per channel (in GUI)
maxsecondsperchannel = 60

#sendreportifprocesserror : do not send a report by mail if only process errors occurred. useful if outcommunication often gives error. default= True (send if there is a process error)
sendreportifprocesserror = True

#imap4debug: print detailed information about imap4 session(s). Default 0 (no debug) (can use 0,1,2,3,4,5)
imap4debug=0

[webserver]

#the server_name. Used to distinguish different bots-environments. defaults: bots-webserver
name = bots-webserver

#in order to use ssl/https:
#    - indicate here the file for the ssl_certificate and ssl_private_key. (both can be in the same file)
#    - uncomment the lines
#(and of course you will have to make the certificate and private key yourself)
#self-signed certificates are allowed.
#ssl_certificate = /path/to/filename
#ssl_private_key = /path/to/filename
```

### Details

More details about version 2.10 are [here](http://bots.sourceforge.net/en/botsversion210.shtml).
