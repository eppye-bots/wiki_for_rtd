Configuration change management (bots>=3.0)
-------------------------------------------

Having different environments for at least test and production is a
sound IT practice. But having different environments also brings
problems:

.. raw:: html

   <ul><li>

push changes in a controlled way to production-environment

.. raw:: html

   </li><li>

are changes done right, and does the existing configuration still run
right?

.. raw:: html

   </li><li>

keep test-environment in line with production-environment To handle
these problems bots has some features called configuration change
management.

.. raw:: html

   </li></ul>

.. raw:: html

   <h2>

Bots configuration change management

.. raw:: html

   </h2>

Configuration change management in bots has 2 aspects:

.. raw:: html

   <ol><li>

Use tools for:

.. raw:: html

   <ul><li>

Comparing differences in configuration of environments

.. raw:: html

   </li><li>

Pushing the changes from test->production environment in a controlled,
automated way

.. raw:: html

   </li></ul></li><li>

Use of isolated acceptance test to:

.. raw:: html

   <ul><li>

check if acceptance test runs OK in test

.. raw:: html

   </li><li>

check if acceptance test runs OK in production

.. raw:: html

   </li><li>

make the test-environment (very) equal to production-environment

.. raw:: html

   </li></ul></li></ol>

Configuration change management works best if both aspects are combined!
See receipe for this!
