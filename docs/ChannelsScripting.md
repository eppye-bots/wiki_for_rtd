## Channel scripting (communicationscripts) 
When the standard communication of bots does not fit your needs, use
communicationscripts.  
Instruction to make a channel script:

1.  there must be channel in bots-monitor (or make a new one)
2.  make a communicationscript with the **same name** as the channelID
3.  place the communicationscript in
    *bots/usersys/communicationscripts/channelid.py*


 Use cases:

-   communication method not provided by bots
-   existing communication needs customization
-   call external program to write edi message to your ERP system.
-   additional requirements: Eg. use partner name or order number in
    output file name.
-   control archive file naming


There are 3 types of communication scripts:

1.  small user exits: at certain places in normal communication a user
    script is called. Examples of 
    [small user exits](CommunicationScriptsExample.md)

2.  subclass: take-over of (parts of) communication script: user script
    subclasses existing communication type.

3.  communication type 'communicationscript'. Bots tries to do the
    bots-handling of files, you provide the communication details. Examples
    of [communication type
    'communicationscript'](CommunicationScriptsType.md)

