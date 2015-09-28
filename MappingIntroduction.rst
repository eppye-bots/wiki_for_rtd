Mapping script
--------------

    Definition: *Instructions to get data from incoming edi-message and
    put it in the outgoing edi-message*

Mapping scripts are python programs. Mapping script are in:
usersys/mappings/editype/mapping script name.py Within a mapping script
function main() is called. Notes:

.. raw:: html

   <ul><li>

All data in the incoming/outgoing messages are strings.

.. raw:: html

   </li><li>

Errors in a mapping script are caught by Bots and displayed in
bots-monitor.

.. raw:: html

   </li><li>

You can Raise an exception in your mapping script if you encounter an
error situation.

.. raw:: html

   </li><li>

(Bots>=3.0) if an error is raised in a script, other translations for
message in same edi-file will continue.

.. raw:: html

   </li><li>

(Bots>=3.0) when an error situation is met in script: you can send
specific error-email to responsible people.
