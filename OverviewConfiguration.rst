Out of the box bots does nothing. You have to configure bots for your
specific edi requirements. Check out different ways to start your own
configuration. See debug overview for info how to debug while making a
configuration. Bots also has nice features for configuration change
management (build test sets for you configuration, easier pushing of
changes from test to production).

.. raw:: html

   <h3>

Configuration explained in short

.. raw:: html

   </h3>
   <ul><li>

'routes' are edi-workflows.

.. raw:: html

   </li><li>

'channels' do the communication (from file system, ftp, etc).

.. raw:: html

   </li><li>

each route hs an 'inchannel' and an 'outchannel'

.. raw:: html

   </li><li>

Translations rules determine: translate what to what.

.. raw:: html

   </li></ul>

.. raw:: html

   <h3>

Most asked configuration topics

.. raw:: html

   </h3>
   <ul><li>

composite routes

.. raw:: html

   </li><li>

passthrough route (without translation)

.. raw:: html

   </li><li>

options for outgoing filenames

.. raw:: html

   </li><li>

direct database communication

.. raw:: html

   </li><li>

partner specific translations

.. raw:: html

   </li><li>

code conversion

.. raw:: html

   </li><li>

view business documents instead of edi-files.

.. raw:: html

   </li><li>

confirmations/acknowledgements

.. raw:: html

   </li><li>

merging and enveloping outgoing edi files

.. raw:: html

   </li><li>

partner specific syntax (especially for x12 and edifact)
