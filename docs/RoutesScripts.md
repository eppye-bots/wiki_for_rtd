## Route scripting

When the standard routing of bots does not fit your needs, use routescripts.

Routescripts are python programs.  
There are 2 types of routescripts:

1.  User exits: at certain points in a route, bots calls your user exit.
    See [overview of exit points](RouteScriptsOverviewExits.md). Most
    common usage is 'pre-processing' an edi file, see
    [recipes](RouteScriptsExample.md).
2.  Your script takes over the whole route. This is done by using
    function *main()* in your routescript. See
    [Example](RouteScriptsExampleWholeRoute.md).

 **How to set up a route-script:**

use bots-monitor to add a new route.

make a routescript with the same name as the routeID in
*bots/usersys/routescripts/`<routeid>`.py*

