# Attributes for routes #

The folloing attributes are used in configuring a route:
  1. Active: only active routes are used when bots-engine runs.
  1. Idroute: identification of the route.
  1. Seq: (for composite routes) determines the sequence for running the route-parts with the same idroute.
  1. Fromchannel: The communication channel bots uses to receive edi-files.
  1. Fromeditype and frommessagetype: The editype and messagetype of the incoming edi-file. Bots uses this to determine the right translation/mapping script.
  1. Alt: (advanced) extra attribute used to determine the translation.
  1. Translate: (for composite routes) indicates if a translation is done in this route-part. A simple route always does a translation.
  1. Tochannel: communication channel used as destination for outbound edi-files.
  1. Defer: set files ready for this communication channel, but communicate these in a route that is run later (and where communication is not deferred. This way all communication for a certain outchannel can be done in one 'session').
  1. Testindicator: (filtering) use only test edi files/production files/both for the outchannel.
  1. Toeditype and Tomessagetype: (filtering) use only this editype/messagetype for the outchannel.
  1. Frompartner\_tochannel and Topartner\_tochannel: (filtering) use only edi-files of this frompartner/topartner for the outchannel.

