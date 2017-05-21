## Introduction

> Definition: _A route is a workflow for edi-files_

A route determines where to get the incoming files, what to do with
these edi-files (translate!) and their destination.  
'Routes' are the most important concept in configuring bots.  
Routes are independent: an edi-file in a route stays in that route.  
Route are configured in *bots-monitor-\>Configuration-\>Routes*.  



> *Schema of a simple route*
>  ![](RouteDiagram2.png)
> 
>  To get a route like this working the following must be configured:

-   the route itself in *bots-monitor-\>Configuration-\>Routes*.
-   an in-channel for incoming edi files.
-   an out-channel for outgoing edi files.
-   the [translation](TranslationIntroduction.md).

The route above is a simple route; files come from one source, there is
one translation, one destination.  
More options are possible using [composite routes](RoutesComposite.md)

