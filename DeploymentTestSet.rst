Build a good test-set
~~~~~~~~~~~~~~~~~~~~~

When you do changes in your edi environment, you want to know that every
'ran as before'. What can be helpful for this is to use a `isolated
acceptance test <DeploymentAcceptance.md>`__ for this.

 This is easy to demonstrate:

.. raw:: html

   <ul><li>

Download a plugin from bots sourceforge site and install it (not on your
production environment;-))

.. raw:: html

   </li><li>

In config/bots.ini set 'runacceptancetest' to True

.. raw:: html

   </li><li>

Run bots-engine via command-line

.. raw:: html

   </li></ul>

 How this works: in acceptance tests an extra script
usersys/routescripts/bots\_acceptancetest.py runs when all routes are
finished. This script does 2 things:

.. raw:: html

   <ul><li>

It compares the results (#files received, errors, send, etc) with the
expected results. If results are different you'll see this (on
command-line window).

.. raw:: html

   </li><li>

The files in botssys/infile/outfile are compared with files as generated
by the run in botssys/outfile. If results are different you'll see this
(on command-line window).

.. raw:: html

   </li></ul>

 Some things to look at when you build a test-set:

.. raw:: html

   <ul><li>

Use the 'acceptance test path' in the channels to point to your file
system for incoming and outgoing channels (prevents using communication
methods like pop3, ftp, etc).

.. raw:: html

   </li><li>

Test file in botssys/infile are added to plugins (I find this very
convenient).

.. raw:: html

   </li><li>

Counters (for message numbers, file names etc (via unique()) are the
same in every run, so results are the same every run.

.. raw:: html

   </li><li>

If date/times need to made, use transform.strftime() for this; it is
like pythons time.strftime() but gives always the same date/time in
acceptance testing.
