Partner specific translation
----------------------------

Explain by example
~~~~~~~~~~~~~~~~~~

You receive edifact ORDERSD96AUNEAN008 from several partners. Partner
'retailer-abroad' fills the orders in a different way; the difference is
so big that it is better to have a separate mapping script. Configure
this like:

.. raw:: html

   <ul><li>

one grammar for incoming edifact ORDERSD96AUNEAN008 message. (It is a
standard message, isn't it?)

.. raw:: html

   </li><li>

one grammar for the inhouse import format. (We definitely want one
import for all orders!)

.. raw:: html

   </li><li>

note that the incoming edifact grammar uses QUERIES to determine the
from-partner and to-partner before the translation.

.. raw:: html

   </li><li>

make the 2 mapping scripts:

.. raw:: html

   <ul><li>

mapping script 'ordersedi2inhouse\_for\_retailerabroad.py' (specific for
partner 'retailer-abroad') .

.. raw:: html

   </li><li>

mapping script 'fixed-myinhouseorder' (for all other retailers).

.. raw:: html

   </li></ul></li><li>

add 'retailer-abroad' to partners (via
bots-monitor->Configuration->Partners & groups).

.. raw:: html

   </li><li>

Use 2 translations rules:

.. raw:: html

   <ul><li>

edifact-ORDERSD96AUNEAN008 to fixed-myinhouseorder using mapping script
ordersedi2inhouse.py

.. raw:: html

   </li><li>

edifact-ORDERSD96AUNEAN008 to fixed-myinhouseorder using mapping script
ordersedi2inhouse\_for\_retailerabroad.py for from-partner
'retailer-abroad'

.. raw:: html

   </li></ul></li></ul>

Often there are lots of similarities between the mappings - the 'many
similar yet different mappings' problems. This can be handled in bots in
a nice way.

.. raw:: html

   <h3>

Plugin

.. raw:: html

   </h3>

Plugin 'demo\_partnerdependent' at the bots sourceforge site
demonstrates partner specific translations.
