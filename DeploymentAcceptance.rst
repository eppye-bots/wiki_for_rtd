Isolated acceptance testing (bots>=3.0)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This is a 'mode' for testing which is **isolated**: \* no external
communication: all I/O is from/to file system \* system state does not
change (eg no increased counters, no test runs in system, etc) Idea is
to run an acceptance test without affecting your system (or the system
of your edi-partner).

**Note**: all plugins since 20130101 are suited for isolated acceptances
tests.

.. raw:: html

   <h3>

Advantages

.. raw:: html

   </h3>
   <ol><li>

Isolated acceptance tests are 'repeatable' (because same counters are
used, same time is used etc). This is great for testing: each run of a
test gives the same results. This makes it easy to compared the results
automatically.

.. raw:: html

   </li><li>

By using isolated acceptance tests your test-environment can be equal to
production-environment. So you can use standard directory comparison
tools to push changes test->production.

.. raw:: html

   </li><li>

As the acceptance tests are isolated, this means an acceptance test can
be run in a production-environment without affecting this environment.
This way you can verify that after a change, all still runs as before in
your production environment.

.. raw:: html

   </li></ol>

.. raw:: html

   <h3>

Running isolated acceptance tests

.. raw:: html

   </h3>
   <ol><li>

in all channels set 'testpath'. Testpath should point to a directory
with test-files.

.. raw:: html

   </li><li>

Set option 'runacceptancetest' in bots.ini to 'True'.

.. raw:: html

   </li><li>

Run 'new'

.. raw:: html

   </li><li>

Check results of run with what you expect

.. raw:: html

   </li><li>

Delete runs/files from acceptance test (menu:Systasks->Bulk delete;
select only 'Delete transactions in acceptance testing'.)

.. raw:: html

   </li></ol>

.. raw:: html

   <h3>

Acceptance tests in plugins

.. raw:: html

   </h3>

Plugins since 20130101 can be run as acceptance tests. About the plugins
with build-in acceptance test:

.. raw:: html

   <ul><li>

'testpath' for incoming files are in botssys

.. raw:: html

   </li><li>

'testpath' for outgoing files go to botssys

.. raw:: html

   </li><li>

each plugin also contains the the expected outgoing files (botssys);
these are used to compare the results.

.. raw:: html

   </li><li>

included is a route script
(bots/usersys/routescripts/bots\_acceptancetest.py):

.. raw:: html

   <ul><li>

before run: discard directory 'botssys'.

.. raw:: html

   </li><li>

after run: global run results are compared with expectation (#in, #out.
#errors, etc)

.. raw:: html

   </li><li>

after run: compare files in botssyswith expected files in botssys

.. raw:: html

   </li><li>

the output of these comparisons can be seen in terminal ('dos-box')

.. raw:: html

   </li></ul></li></ul>

.. raw:: html

   <h3>

Implementation Details

.. raw:: html

   </h3>

What bots does when running an isolated acceptance test:

.. raw:: html

   <ul><li>

channel-type is set to 'file'.

.. raw:: html

   </li><li>

channel-path is set to the value in 'testpath'. if testpath is empty:
use path.

.. raw:: html

   </li><li>

channel-remove is set to 'off': no deletion of incoming files.

.. raw:: html

   </li><li>

error-email: not send.

.. raw:: html

   </li><li>

fixed date/time in envelopes and in mappings (if function
transform.strftime() is used)

.. raw:: html

   </li><li>

counters/references: fixed; counters are not incremented

.. raw:: html

   </li><li>

incoming files are always read in same order.

.. raw:: html

   </li><li>

outgoing-filename options: date/time is fixed

.. raw:: html

   </li><li>

no archiving

.. raw:: html

   </li><li>

additional user exits are run. User exits are in file
usersys/routescripts/botsacceptancetest.py :

.. raw:: html

   <ul><li>

before run:: function pretest. use eg to empty out-directories etc

.. raw:: html

   </li><li>

after run: function post-test. This can be used to check results,
compare files etc After running an isolated acceptance test, the
reports/filereports/data-files/etc generated during acceptance-testing
can be deleted via: menu:Systasks->Bulk delete; select only 'Delete
transactions in acceptance testing'.

.. raw:: html

   </li></ul></li></ul>

Implementation remarks:

.. raw:: html

   <ul><li>

GUI does not have the results of post-test script (runs after
automaticmaintanance); view this in terminal/dos-box.

.. raw:: html

   </li><li>

communication scripts: script should check explicitly if in acceptance
test and act accordingly.

.. raw:: html

   </li><li>

database communication: script should check explicitly if in acceptance
test and act accordingly.
