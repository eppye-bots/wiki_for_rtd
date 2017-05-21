## Partner dependent syntax 

For outgoing messages it is possible to specify a partner dependent syntax.  
This is especially useful for x12 and edifact, for setting envelope
values and partner specific separators.  
These parameters override the settings in the message grammar; you only
need to specify the partner-specific parameters.  
Note: no need to set partner specific separators for incoming messages;
bots will figure this out by itself.  
To set partner specific syntax parameters, create according to editype
used:

-   *bots/usersys/partners/x12/partnerid.py*
-   *bots/usersys/partners/edifact/partnerid.py*

Example file with partner specific setting (x12):

>     syntax = {
>     'ISA05'                  : 'XX',    #use different communication qualifier for sender
>     'ISA07'                  : 'ZZ',    #use different communication qualifier for receiver
>     'field_sep'              : '|',     #use different field separator
>     }

Example file with partner specific setting (edifact):

>     syntax = {
>     'merge':False,
>     'forceUNA':True,
>     'UNB.S002.0007':'ZZ',        # partner qualifier
>     'UNB.S003.0007':'ZZ',        # partner qualifier
>     }



### Plugin

Plugin 'demo\_partnerdependent' at [the bots sourceforge
site](http://sourceforge.net/projects/bots/files/plugins/) demonstrates
partner dependent syntax.


### Relevant x12 syntax settings

Name           |Default|Description
---------------|-------|------------
ISA05          |01     |Interchange ID Sender Qualifier
ISA07          |01     |Interchange ID Receiver Qualifier
ISA15          |P      |Testindicator: P(roduction) or T(est); mostly set per message/transaction.
GS07           |X      |Responsible Agency Code
version        |00403  |As ISA12
functionalgroup|       |As GS01; set this for each x12 messagetype
record\_sep    | ~     |Segment terminator.
field\_sep     |`*`    |
sfield\_sep    |\>     |Sub-field separator (in composites).
merge          |True   |Merge messages to envelopes (False: no merging, only envelope).
add\_crlfafterrecord\_sep|\\r\\n|Adds CR/LF after each segment.



### Relevant edifact syntax settings

Name           |Default|Description
---------------|-------|------------
UNB.S002.0007  |14     |Identification code qualifier
UNB.S002.0008  |       |Interchange sender internal identification
UNB.S002.0042  |       |Interchange sender internal sub-identification
UNB.S003.0007  |14     |Identification code qualifier
UNB.S003.0014  |       |Interchange recipient internal identification
UNB.S003.0046  |       |Interchange recipient internal sub-identification
UNB.S005.0022  |       |Recipient reference/password
UNB.S005.0025  |       |Recipient reference/password qualifier
UNB.0026       |       |Application reference
UNB.0029       |       |Processing priority code
UNB.0031       |       |Acknowledgement request
UNB.0032       |       |Interchange agreement identifier (eg. EANCOM)
UNB.0035       |0      |Testindicator. Mostly set per message.
charset        |UNOA   |As S001.0001
version        |3      |As S001.0002
merge          |True   |Merge messages to envelopes (False: no merging, only envelope).
forceUNA       |False  |Always use UNA in outgoing edifact, even if not strictly needed.
add\_crlfafterrecord\_sep|\\r\\n|Adds CR/LF after each segment.

