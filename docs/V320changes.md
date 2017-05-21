## List of changes bots 3.2.0 ##

### Highlights ###
  1. added http(s) communication to communication methods (using 'requests' library).
  1. better reporting of partnerID for incoming files with errors.
  1. file rename after outcommunication using tmp filenames to avoid 'reading before writing'.
  1. updated edifax (print to html); is much easier to use now (edifax plugin will be updated).

### Interface (GUI) ###
  1. in run-screen: show used command for bots-engine, show if acceptance test.
  1. search by filename for incoming and outgoing files.
  1. 'strange characters' like ëë in routeID, channelID, etc will work now.
  1. option to have automaticretrycommunication in menu.
  1. option to add only routes that are not in default run to menu.
  1. added bulk delete for persists data.
  1. use 'rereceive' and 'resend' in screens (instead of 'retransmit').
  1. simpler making bots suited for touchscreen.
  1. filter routes for (not) in default run.
  1. improved edifact indenting in file viewer.
  1. div small layout improvements in GUI.

### Smaller changes ###
  1. unicode handling is improved. This is about use of unicode in route-names, grammars, correct errors, etc
  1. set maxdaysarchive per channel.
  1. email validation in django was too strict for certain email addresses.
  1. check CC-address when validating incoming email-addresses.
  1. improve reporting on in-communication failures (give process-error after x time failure).
  1. suited for django 1.4, 1.5, 1.6and 1.7. Django 1.3 support is dropped.
  1. add incoming filename in email-report.
  1. option to use user script entries at start/end of a run and command.
  1. added option 'parse and passthrough' for routes. Useful for eg generating 997/CONTROL.
  1. added explicit enveloping indication (this indication can be set in mapping).
  1. making of plugin could take take a long time (better performance for large plugins).
  1. improve processing of repeat separator in ISA version above 00403.
  1. xml2botsgrammar: order of elements is preserved now; all xml entities as records.
  1. xml2botsgrammar: added option to have all xml entities as 'record'.
  1. added option to have function 'transform.partnerlookup' return 'None' if not found.
  1. improve xmlrpc communication.
  1. for persist: change timestamp on update.
  1. used new definitions for UNOA and UNOB. Definitions are clearer and easier to change, no change in functionality.
  1. better performance for one-on-one translations.
  1. bots-engine uses less memory.
  1. better reporting for import errors.

### Bug fixes ###
  1. preprocessing not working for rereceive.
  1. fixed bug in windows installer (occurred when when UAC is disabled).
  1. routeid did not always show up correct in error.
  1. rights problem: viewer can delete incoming files.
  1. show filesize for passthrough files.
  1. MySQLdb version 1.2.5 gave error.
  1. change password for non-staff user did not work.
  1. found query's in GUI not using index (better performance).
  1. error could not be displayed: <unprintable MessageError object>.
  1. multiple email-addresses were not used in sending emails.
  1. transform.concat erroneously added spaces between elements.
  1. callable in QUERIES should have 'node' as parameter.
  1. when received x12 message can not be parsed correctly, GS08 might not be found.
  1. routeid did not show up correct in some errors.
  1. incoming tab-delimited file not parsed correct (for nobotsID & first field Conditional).
  1. via incoming/outgoing screen: button 'confirm (same selection)' did not work.
  1. in forms.py: reference was an..35, should be an..70
