Several situations: \* send different versions of messages \* receive
different versions Note: in real world versions are often so similar
that the same mapping script can be used (or a simple if-then can cater
for the differences).

.. raw:: html

   <h3>

Send multiple versions using partners

.. raw:: html

   </h3>

use the 'topartner' to determine the right version to send.

.. raw:: html

   <ul><li>

one grammar for in-house message:

.. raw:: html

   <ul><li>

myinhouseorder.py

.. raw:: html

   </li><li>

this grammar uses QUERIES to extract 'topartner'.

.. raw:: html

   </li></ul></li><li>

grammars for both versions:

.. raw:: html

   <ul><li>

ORDERSD93AUN

.. raw:: html

   </li><li>

ORDERSD96AUN

.. raw:: html

   </li></ul></li><li>

2 translation rules:

.. raw:: html

   <ul><li>

fixed-myinhouseorder to edifact-ORDERSD93AUN using mapping script
ordersfixed2edifact93.py for topartner=XXX

.. raw:: html

   </li><li>

fixed-myinhouseorder to edifact-ORDERSD96AUN using mapping script
ordersfixed2edifact93.py for topartern=YYY

.. raw:: html

   </li></ul></li></ul>

.. raw:: html

   <h3>

Send multiple versions using alt

.. raw:: html

   </h3>

Information about the version is in in-house-message: a field that
contains either '93' or '96'.

.. raw:: html

   <ul><li>

one grammar for in-house message:

.. raw:: html

   <ul><li>

myinhouseorder.py

.. raw:: html

   </li></ul></li><li>

grammars for both versions:

.. raw:: html

   <ul><li>

ORDERSD93AUN

.. raw:: html

   </li><li>

ORDERSD96AUN

.. raw:: html

   </li></ul></li><li>

2 translation rules

.. raw:: html

   <ul><li>

fixed-myinhouseorder to edifact-ORDERSD93AUN using mapping script
orders\_fixed2edifact93.py for alt=93

.. raw:: html

   </li><li>

fixed-myinhouseorder to edifact-ORDERSD96AUN using mapping script
orders\_fixed2edifact93.py for alt=96

.. raw:: html

   </li></ul></li></ul>

.. raw:: html

   <h3>

Receive multiple versions

.. raw:: html

   </h3>
   <ul><li>

grammars for both versions:

.. raw:: html

   <ul><li>

ORDERSD93AUN

.. raw:: html

   </li><li>

ORDERSD96AUN

.. raw:: html

   </li></ul></li><li>

one grammar for in-house message:

.. raw:: html

   <ul><li>

myinhouseorder.py

.. raw:: html

   </li><li>

this grammar uses QUERIES to extract 'alt'-value.

.. raw:: html

   </li></ul></li><li>

2 translation rules

.. raw:: html

   <ul><li>

edifact-ORDERSD93AUN to fixed-myinhouseorder using mapping script
orders\_edifact93\_2\_fixed.py

.. raw:: html

   </li><li>

edifact-ORDERSD6AUN to fixed-myinhouseorder using mapping script
orders\_edifact96\_2\_fixed.py
