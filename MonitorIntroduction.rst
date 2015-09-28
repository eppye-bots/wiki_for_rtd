Note: the `tutorial <StartMyFirstPlugin.md>`__ contains some detailed
information and screen-shots of bots-monitor!

.. raw:: html

   <h2>

Menu in bots-monitor

.. raw:: html

   </h2>

   <ol><li>

Home: start page and general information.

.. raw:: html

   </li><li>

Last run: view results of the last run:

.. raw:: html

   <ul><li>

incoming: view incoming files and results

.. raw:: html

   </li><li>

document: view status of business document. An edi file can contain
multiple documents (eg orders). In this view are the results of the
separate business documents. See setting document views

.. raw:: html

   </li><li>

outgoing: view outgoing files and results

.. raw:: html

   </li><li>

process errors: view process errors; mostly these will be communication
errors.

.. raw:: html

   </li></ul></li><li>

All runs: view results of all runs:

.. raw:: html

   <ul><li>

reports: view of all runs and results

.. raw:: html

   </li><li>

incoming: view incoming files and results

.. raw:: html

   </li><li>

document: view status of business document. An edi file can contain
multiple documents (eg orders). In this view are the results of the
separate business documents. See setting document views

.. raw:: html

   </li><li>

outgoing: view outgoing files and results

.. raw:: html

   </li><li>

process errors: view process errors; mostly these will be communication
errors.

.. raw:: html

   </li><li>

confirmations: view the results of confirmations you wanted and
confirmation you gave. See setup confirmations

.. raw:: html

   </li></ul></li><li>

Select: use criteria like date/time to view results you want to see like
eg editype edifact or x12.

.. raw:: html

   <ul><li>

Note: select screens can also be used using 'select' button in other
views.

.. raw:: html

   </li></ul></li><li>

Configuration: configuration of the edi setup.

.. raw:: html

   </li><li>

System tasks (administrators only): read plugins, create plugins,
maintain users, etc.

.. raw:: html

   </li><li>

Run: manually start a run of bots-engine:

.. raw:: html

   <ul><li>

Run (only new): receive, translate, and send new edi messages.

.. raw:: html

   </li><li>

Run userindicated rerecieves: receive previously received edi-files
again from archive. User has to mark edi-files as 're-receive' via
incoming view.

.. raw:: html

   </li><li>

Run userindicated resends: resend previously send edi-files again. User
has to mark edi-files as 're-send' via outgoing view.

.. raw:: html

   </li></ul></li></ol>

.. raw:: html

   <h2>

User interface tips

.. raw:: html

   </h2>
   <ul><li>

View screens often have a star at the beginning of each line; moving
over the star will show possible actions.

.. raw:: html

   </li><li>

In view screens, you can see the contents of an edi file if you click on
the file name.

.. raw:: html

   </li><li>

When viewing the contents of an edi file, you can go backwards and
forwards to see the processing steps of the file.

.. raw:: html

   </li><li>

Might be handy to use tabbed browsing.

.. raw:: html

   </li><li>

Bots uses user rights (viewers, administrators and superuser). See
setting user rights
