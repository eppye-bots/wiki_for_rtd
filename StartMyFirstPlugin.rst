Purpose of this tutorial is to get your first edi configuration running.
This is done by installing plugin 'my\_first\_plugin'; this plugin
provides a working configuration. When run, this configuration will read
and write example edi messages (provided in the plugin) from your
system. In this configuration incoming edifact orders are translated to
a fixed file format.

.. raw:: html

   <h2>

Install plugin 'my\_first\_plugin'

.. raw:: html

   </h2>

Assumed is:

.. raw:: html

   <ol><li>

You've installed bots, see installation

.. raw:: html

   </li><li>

You've managed to get bots-monitor running, see get bots running.

.. raw:: html

   </li></ol>

Now download and install plugin 'my\_first\_plugin'. Instructions for
installing a plugin are here. The plugin can be downloaded from the bots
sourceforge site.

.. raw:: html

   <h2>

Activate the route

.. raw:: html

   </h2>
   <ol><li>

go to the routes screen: bots-monitor->Configuration->Routes

.. raw:: html

   </li><li>

note that route 'myfirstroute' is not active now (indicated by red icon)

.. raw:: html

   </li><li>

select the tick-box in front of the route 'myfirstroute'

.. raw:: html

   </li><li>

select action 'activate/de-activate'

.. raw:: html

   </li><li>

click on the 'Go'-button behind the selected action.

.. raw:: html

   </li><li>

note that route 'myfirstroute' is active now (indicated by green icon)

.. raw:: html

   </li></ol>

.. raw:: html

   <h2>

Run the translation

.. raw:: html

   </h2>

Run the translation: bots-monitor->Run->Run (Only New). You will get
notified that the bots-engine is started. Bots-engine is the part of
bots that does the translations and communications; it runs in the
background. Bots-engine will be finished in approximately one second.

.. raw:: html

   <h2>

View the results

.. raw:: html

   </h2>

Now let's view the results of the translation:

.. raw:: html

   <ul><li>

First look at the results of the run: bots-monitor->All runs->Reports
(per run). Each run of bots is represented by a line; the last run is on
top.

.. raw:: html

   </li><li>

View the incoming files via bots-monitor->Last run->Incoming. Click on
the incoming file to see its contents.

.. raw:: html

   </li><li>

View the outgoing files (the results of the translation) go to or
bots-monitor->Last run->outgoing. Again: click on the file name to see
its contents.

.. raw:: html

   </li></ul>

Note: this configuration reads the incoming files but does not delete
them. So you can run it over and over again.

.. raw:: html

   <h2>

More

.. raw:: html

   </h2>
   <ul><li>

Screenshots and information about viewing the results.

.. raw:: html

   </li><li>

Walk through the configuration in this plugin is here.

.. raw:: html

   </li><li>

A more detailed explanation about the 'run' and what happens in a run is
here.

.. raw:: html

   </li></ul>





