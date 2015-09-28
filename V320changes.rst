List of changes bots 3.2.0
--------------------------

Highlights
~~~~~~~~~~

1. added http(s) communication to communication methods (using
   'requests' library).
2. better reporting of partnerID for incoming files with errors.
3. file rename after outcommunication using tmp filenames to avoid
   'reading before writing'.
4. updated edifax (print to html); is much easier to use now (edifax
   plugin will be updated).

Interface (GUI)
~~~~~~~~~~~~~~~

1.  in run-screen: show used command for bots-engine, show if acceptance
    test.
2.  search by filename for incoming and outgoing files.
3.  'strange characters' like ëë in routeID, channelID, etc will work
    now.
4.  option to have automaticretrycommunication in menu.
5.  option to add only routes that are not in default run to menu.
6.  added bulk delete for persists data.
7.  use 'rereceive' and 'resend' in screens (instead of 'retransmit').
8.  simpler making bots suited for touchscreen.
9.  filter routes for (not) in default run.
10. improved edifact indenting in file viewer.
11. div small layout improvements in GUI.

Smaller changes
~~~~~~~~~~~~~~~

1.  unicode handling is improved. This is about use of unicode in
    route-names, grammars, correct errors, etc
2.  set maxdaysarchive per channel.
3.  email validation in django was too strict for certain email
    addresses.
4.  check CC-address when validating incoming email-addresses.
5.  improve reporting on in-communication failures (give process-error
    after x time failure).
6.  suited for django 1.4, 1.5, 1.6and 1.7. Django 1.3 support is
    dropped.
7.  add incoming filename in email-report.
8.  option to use user script entries at start/end of a run and command.
9.  added option 'parse and passthrough' for routes. Useful for eg
    generating 997/CONTROL.
10. added explicit enveloping indication (this indication can be set in
    mapping).
11. making of plugin could take take a long time (better performance for
    large plugins).
12. improve processing of repeat separator in ISA version above 00403.
13. xml2botsgrammar: order of elements is preserved now; all xml
    entities as records.
14. xml2botsgrammar: added option to have all xml entities as 'record'.
15. added option to have function 'transform.partnerlookup' return
    'None' if not found.
16. improve xmlrpc communication.
17. for persist: change timestamp on update.
18. used new definitions for UNOA and UNOB. Definitions are clearer and
    easier to change, no change in functionality.
19. better performance for one-on-one translations.
20. bots-engine uses less memory.
21. better reporting for import errors.

Bug fixes
~~~~~~~~~

1.  preprocessing not working for rereceive.
2.  fixed bug in windows installer (occurred when when UAC is disabled).
3.  routeid did not always show up correct in error.
4.  rights problem: viewer can delete incoming files.
5.  show filesize for passthrough files.
6.  MySQLdb version 1.2.5 gave error.
7.  change password for non-staff user did not work.
8.  found query's in GUI not using index (better performance).
9.  error could not be displayed: .
10. multiple email-addresses were not used in sending emails.
11. transform.concat erroneously added spaces between elements.
12. callable in QUERIES should have 'node' as parameter.
13. when received x12 message can not be parsed correctly, GS08 might
    not be found.
14. routeid did not show up correct in some errors.
15. incoming tab-delimited file not parsed correct (for nobotsID & first
    field Conditional).
16. via incoming/outgoing screen: button 'confirm (same selection)' did
    not work.
17. in forms.py: reference was an..35, should be an..70

