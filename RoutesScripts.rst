Route scripting
---------------

When the standard routing of bots does not fit your needs, use
routescripts. Routescripts are python programs.

There are 2 types of routescripts:

.. raw:: html

   <ol><li>

User exits: at certain points in a route, bots calls your user exit. See
overview of exit points. Most common usage is 'pre-processing' an edi
file, see recipes.

.. raw:: html

   </li><li>

Your script takes over the whole route. This is done by using function
main() in your routescript. See Example.

.. raw:: html

   </li></ol>

How to set up a route-script:

.. raw:: html

   <ol><li>

use bots-monitor to add a new route.

.. raw:: html

   </li><li>

make a routescript with the same name as the routeID in
bots/usersys/routescripts/<routeid>.py
