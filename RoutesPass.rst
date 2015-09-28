Sometimes you want to pass an edi-file though bots without translation.
In this case bots is only used to manage/register the sending or
receiving of edi-files.

.. raw:: html

   <h3>

for bots>=3.0

.. raw:: html

   </h3>

In route (bots-monitor->Configuration->Routes) use value 'Pass-through'
for 'translate'.

.. raw:: html

   <h3>

for bots<=2.2

.. raw:: html

   </h3>

Use a routescript:

.. raw:: html

   <ol><li>

configure route the normal way (bots-monitor->Configuration->Routes)

.. raw:: html

   </li><li>

make a routescript with the same name as the routeID

.. raw:: html

   </li><li>

place the routescript in bots/usersys/routescripts/routeid.py

.. raw:: html

   </li></ol>

Contents of routescript:

.. raw:: html

   <pre><code>from bots.botsconfig import *<br>
   import bots.transform as transform<br>
   <br>
   def postincommunication(routedict,*args,**kwargs): <br>
       # postincommunication() is run after fromchannel communication.<br>
       # the status of incoming files is changed to outgoing. <br>
       # bots skips parsing and translation.<br>
       transform.addinfo(change={'status':MERGED},where={'status':FILEIN,'idroute':routedict['idroute']})<br>
   </code></pre>

