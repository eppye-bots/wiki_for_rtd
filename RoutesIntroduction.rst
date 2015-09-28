Introduction
------------

    Definition: *A route is a workflow for edi-files*

    .. raw:: html

       </li></ul>

A route determines where to get the incoming files, what to do with
these edi-files (translate!) and their destination. 'Routes' are the
most important concept in configuring bots. Routes are independent: an
edi-file in a route stays in that route. Route are configured in
bots-monitor->Configuration->Routes.

.. raw:: html

   <blockquote>

Schema of a simple route To get a route like this working the following
must be configured:

.. raw:: html

   </blockquote><ul><li>

the route itself in bots-monitor->Configuration->Routes.

.. raw:: html

   </li><li>

an in-channel for incoming edi files.

.. raw:: html

   </li><li>

an out-channel for outgoing edi files.

.. raw:: html

   </li><li>

the translation.

.. raw:: html

   </li></ul>

The route above is a simple route; files come from one source, there is
one translation, one destination. More options are possible using
composite routes
