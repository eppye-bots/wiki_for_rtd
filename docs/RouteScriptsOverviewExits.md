### List of Exit Points in Routes ###

These examples show all of the available exit points for route-scripts

```
def start(routedict,*args,**kwargs): 
    # run before anything is done is route.
    print routedict['idroute'],'start'

def preincommunication(routedict,*args,**kwargs): 
    # if there is a fromchannel: run before fromchannel communication.
    print routedict['idroute'],'preincommunication'

def postincommunication(routedict,*args,**kwargs): 
    # if there is a fromchannel: run after fromchannel communication.
    print routedict['idroute'],'postincommunication'

def pretranslation(routedict,*args,**kwargs): 
    # if translation is done in route: run before translation.
    print routedict['idroute'],'pretranslation'

def posttranslation(routedict,*args,**kwargs): 
    # if translation is done in route: run after translation.
    print routedict['idroute'],'posttranslation'

def premerge(routedict,*args,**kwargs): 
    # if there is a outchannel: run before merging.
    print routedict['idroute'],'premerge'

def postmerge(routedict,*args,**kwargs): 
    # if there is a outchannel: run after merging.
    print routedict['idroute'],'postmerge'

def preoutcommunication(routedict,*args,**kwargs): 
    # if there is a outchannel: run before outchannel communication.
    print routedict['idroute'],'preoutcommunication'

def postoutcommunication(routedict,*args,**kwargs): 
    # if there is a outchannel: run after outchannel communication.
    # eg. call an external program to process files just sent into ERP system
    print routedict['idroute'],'postoutcommunication'

def end(routedict,*args,**kwargs): 
    # after everything is done in route
    print routedict['idroute'],'end'
```