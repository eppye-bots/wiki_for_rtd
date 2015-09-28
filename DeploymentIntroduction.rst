Deployment
==========

This part of the wiki is about using bots in production.

There are extra points to consider when deploying bots in a 24x7
production environment:

.. raw:: html

   <ol><li>

Consider the best way of running bots-engine.

.. raw:: html

   </li><li>

When errors in edi-files occur, receive a notification by email.

.. raw:: html

   </li><li>

Use multiple environments; having different environments for at least
test and production is standard IT practice.

.. raw:: html

   </li><li>

Consider if edi files need extra archiving

.. raw:: html

   </li><li>

Out of the box bots does not run as a service/daemon. In a production
enviroment this is what you'll probably want.
