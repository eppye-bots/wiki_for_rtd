## List of changes ##

### Interface (GUI) ###
  1. Improved and simplified many screens. Eg only filename is displayed (takes less space), a pop-up show full path name
    1. incoming
    1. outgoing
    1. detail
    1. document; split up to incoming and outgoing screens;
    1. confirm
  1. Show in configuration screen if there are routescripts, communicationscripts, mappingscripts, grammars. Routescripts etc can be viewed.
  1. Partners and partnergroups are split up (via menu and screens).
  1. Added a cancel button in configuration editing.
  1. Added a choice list for routes in Configuration-Confirm.
  1. Display edifact/x12: display per segment for better readability.
  1. Show correct number of messages for resends.
  1. Email error report is extended with information about errors.
  1. Improved view/edit counters screen.
  1. In errors the correct name of eg grammars is shown. This was confusing (using sometimes '.' instead of '\' etc).

### Highlights ###
  1. Extra debug option: check all get/getloop if OK with grammars.
  1. Support for repeating elements is added (x12/edifact).
  1. Simplified logic of syntax reading: default syntax is overridden by envelope syntax is overridden by message sytax is overridden by partner-syntax.
  1. Added: fixed records can now be 'nobotsid': one record type, split to messages via field.
  1. Generating 997's can be done/manipulated via user script .

### Smaller changes ###
  1. Skip empty json elements in incoming files.
  1. StartrecordID and endrecordID are not needed anymore for in grammars for fixed message/idoc, bots calculates this now.
  1. Small improvements and bug fixes in XML reading/writing.
  1. QUERIES now also support callables.
  1. Xml2botsgrammar: sort fields in recorddefs, use empty elements in grammar.
  1. If 'alt' transaltion is not found, use default translation.
  1. More consistent handling of exceptions and logging (coding only).
  1. Fixed problems starting bots-engine from webserver in less common situations.
  1. Get correct incoming filename for re-receive.
  1. Removed code for old database connector and code-conversion via file.
  1. Automaticretry: first run only initialization (to avoid sending moch older files).
  1. Explicitly set for outgoing file: no automatic retry.
  1. Plugins: for different environments, path and testpath in channels are also relocated .
  1. Plugins: handling of unicode-characters is now correct.
  1. Add mapping function: getdecimal(). Returns a python decimal; if not found or non-valid input: returns decimal 0.
  1. For csv and fixed with 'noBOTSID': nextmessageblock can check for multiple fields, eg: nextmessageblock = ([{'BOTSID':'lin','field1':None},{'BOTSID':'lin','field2':None}])
  1. When deleting configuration items via 'bulk delete': make a backup plugin first.



### Bug fixes ###
  1. There was a missing import in xml2botsgrammar
  1. Logging of mapping debug did not work in 3.0
  1. Correct handling of resends/rereceives for already resend/received files
  1. Fixed bug in automaticretrycommunication
  1. Confirmation can now be asked via channel-rule.
  1. if multiple commands in run: reports etc are based on timestamp. This messed up the relation between runs and eg incoming files.