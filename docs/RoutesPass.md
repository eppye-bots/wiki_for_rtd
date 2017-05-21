## Routes pass through

Sometimes you want to pass an edi-file through bots without translation.

In this case bots is only used to manage/register the sending or
receiving of edi-files.


### for bots \>= 3.0

In route (*bots-monitor-\>Configuration-\>Routes*) use value
'Pass-through' for 'translate'.


### for bots \<= 2.2

Use a routescript:

1.  configure route the normal way
    (*bots-monitor-\>Configuration-\>Routes*)
2.  make a routescript with the same name as the routeID
3.  place the routescript in *bots/usersys/routescripts/routeid.py*

Contents of routescript:

    from bots.botsconfig import *
    import bots.transform as transform

    def postincommunication(routedict,*args,**kwargs): 
        # postincommunication() is run after fromchannel communication.
        # the status of incoming files is changed to outgoing. 
        # bots skips parsing and translation.
        transform.addinfo(change={'status':MERGED},where={'status':FILEIN,'idroute':routedict['idroute']})
