Channel scripting (communicationscripts)
========================================

When the standard communication of bots does not fit your needs, use
communicationscripts.

Instruction to make a channel script:

.. raw:: html

   <ol><li>

there must be channel in bots-monitor (or make a new one)

.. raw:: html

   </li><li>

make a communicationscript with the same name as the channelID

.. raw:: html

   </li><li>

place the communicationscript in
bots/usersys/communicationscripts/channelid.py

.. raw:: html

   </li></ol>

 Use cases:

.. raw:: html

   <ul><li>

communication method not provided by bots

.. raw:: html

   </li><li>

existing communication needs customization

.. raw:: html

   </li><li>

call external program to write edi message to your ERP system.

.. raw:: html

   </li><li>

additional requirements: Eg. use partner name or order number in output
file name.

.. raw:: html

   </li><li>

control archive file naming

.. raw:: html

   </li></ul>

 There are 3 types of communication scripts:

.. raw:: html

   <ol><li>

small user exits: at certain places in normal communication a user
script is called. Examples of small user exits

.. raw:: html

   </li><li>

subclass: take-over of (parts of) communication script: user script
subclasses existing communication type.

.. raw:: html

   </li><li>

communication type 'communicationscript'. Bots tries to do the
bots-handling of files, you provide the communication details. Examples
of communication type 'communicationscript'
