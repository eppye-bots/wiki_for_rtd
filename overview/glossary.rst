Glossary of Terms
=================

.. csv-table::

    "alt","Used for chained translations."
    "botskey","Used for business document number, eg order number, invoice number. Used to set up :doc:`document views <../configuration/document-view>` (view business document level)."
    "channel type","Type of communication used for sending/receiving files like ftp, smtp, file I/O."
    "chained translation","A chained translations translate one incoming format to multiple outgoing formats."
    "editype","Type of edi-file like x12, edifact, tradacoms, xml, csv, fixed record files."
    "mapping script","A python script containing instructions how to get data from incoming edi-message and put it in the outgoing edi-message."
    "messagetype","eg 850 (an x12 order), ORDERSD96AUN (edifact order) or your inhouse xml-orders. A messagetype is defined in a grammar"
    "route","a workflow for edi-files"
    "translation","convert a message of a certain editype, messagetype to another editype, messagetype using a mapping script."
    "translation rule","determines what translations are done for incoming files. In ``bots-monitor->Configuration->Translations``"
