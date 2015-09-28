What translation when?
----------------------

Bots figures out what translation to use via the translation rules. Best
is to think of the translation rules as a 'lookup' table:

.. raw:: html

   <blockquote>

look-up with (from-editype, from-messagetype, alt, frompartner and
topartner) to find mappingscript, to-editype and to-messagetype

.. raw:: html

   </blockquote>

 How the input values for the look-up are determined:

.. raw:: html

   <ol><li>

editype

.. raw:: html

   <ul><li>

configured in the route

.. raw:: html

   </li><li>

if you configure editype=mailbag, bots will figure out if editype is
x12, edifact or tradacoms.

.. raw:: html

   </li></ul></li><li>

messagetype can be:

.. raw:: html

   <ul><li>

configured in the route, eg for editype csv

.. raw:: html

   </li><li>

for edifact, x12 and tradacoms: bots figures out the detailed
messagetype. Example:

.. raw:: html

   <ul><li>

in route: editype: edifact, messagetype: edifact

.. raw:: html

   </li><li>

in incoming edi file bots finds detail messagetype 'ORDERSD96AUN'.

.. raw:: html

   </li></ul></li></ul></li><li>

frompartner can be:

.. raw:: html

   <ul><li>

configured in the route

.. raw:: html

   </li><li>

determined by the grammar using QUERIES

.. raw:: html

   </li></ul></li><li>

topartner can be:

.. raw:: html

   <ul><li>

configured in the route

.. raw:: html

   </li><li>

determined by the grammar using QUERIES

.. raw:: html

   </li></ul></li><li>

alt can be:

.. raw:: html

   <ul><li>

configured in the route

.. raw:: html

   </li><li>

determined by the grammar using QUERIES

.. raw:: html

   </li><li>

set by mapping script in a chained translation

.. raw:: html

   </li></ul></li></ol>

 Notes:

.. raw:: html

   <ul><li>

For frompartner and topartner: bots finds the most specific translation.

.. raw:: html

   <ul><li>

Eg example with 2 translation rules:

.. raw:: html

   <ul><li>

fromeditype = edifact, frommessagetype = ORDERSD96AUNEAN008

.. raw:: html

   </li><li>

fromeditype = edifact, frommessagetype = ORDERSD96AUNEAN008,
frompartner=RETAILERX

.. raw:: html

   </li></ul></li><li>

If bots receives an ORDERS message from RETAILERX, the 2nd translation
is used.

.. raw:: html

   </li><li>

For other partners the first translation is used.

.. raw:: html

   </li></ul></li></ul>

   <ul><li>

for alt-translations: only find the translation with that specific
'alt'.
