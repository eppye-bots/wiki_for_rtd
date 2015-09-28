Introduction
------------

    Definition: *A translation translates a message of a certain
    editype, messagetype to another editype, messagetype*

Needed for a translation: 1. Translation rule in
*bots-monitor->Configuration->Translations*; see the screen shot below.
1. `Grammar <GrammarsIntroduction.md>`__ for incoming message. 1.
`Grammar <GrammarsIntroduction.md>`__ for outgoing message. 1. Mapping
script that for converting incoming message to outgoing message.

.. raw:: html

   <blockquote>

Screenshot of configured translations-rules

.. raw:: html

   </blockquote>

Read the 1st translation rule of this screen shot:

.. raw:: html

   <blockquote>

translate edifact-ORDERSD96AUNEAN008 to fixed-myinhouseorder using
mapping script ordersedifact2myinhouse.py
