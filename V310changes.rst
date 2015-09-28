List of changes
---------------

Interface (GUI)
~~~~~~~~~~~~~~~

1.  Improved and simplified many screens. Eg only filename is displayed
    (takes less space), a pop-up show full path name

    1. incoming
    2. outgoing
    3. detail
    4. document; split up to incoming and outgoing screens;
    5. confirm

2.  Show in configuration screen if there are routescripts,
    communicationscripts, mappingscripts, grammars. Routescripts etc can
    be viewed.
3.  Partners and partnergroups are split up (via menu and screens).
4.  Added a cancel button in configuration editing.
5.  Added a choice list for routes in Configuration-Confirm.
6.  Display edifact/x12: display per segment for better readability.
7.  Show correct number of messages for resends.
8.  Email error report is extended with information about errors.
9.  Improved view/edit counters screen.
10. In errors the correct name of eg grammars is shown. This was
    confusing (using sometimes '.' instead of '' etc).

Highlights
~~~~~~~~~~

1. Extra debug option: check all get/getloop if OK with grammars.
2. Support for repeating elements is added (x12/edifact).
3. Simplified logic of syntax reading: default syntax is overridden by
   envelope syntax is overridden by message sytax is overridden by
   partner-syntax.
4. Added: fixed records can now be 'nobotsid': one record type, split to
   messages via field.
5. Generating 997's can be done/manipulated via user script .

Smaller changes
~~~~~~~~~~~~~~~

1.  Skip empty json elements in incoming files.
2.  StartrecordID and endrecordID are not needed anymore for in grammars
    for fixed message/idoc, bots calculates this now.
3.  Small improvements and bug fixes in XML reading/writing.
4.  QUERIES now also support callables.
5.  Xml2botsgrammar: sort fields in recorddefs, use empty elements in
    grammar.
6.  If 'alt' transaltion is not found, use default translation.
7.  More consistent handling of exceptions and logging (coding only).
8.  Fixed problems starting bots-engine from webserver in less common
    situations.
9.  Get correct incoming filename for re-receive.
10. Removed code for old database connector and code-conversion via
    file.
11. Automaticretry: first run only initialization (to avoid sending moch
    older files).
12. Explicitly set for outgoing file: no automatic retry.
13. Plugins: for different environments, path and testpath in channels
    are also relocated .
14. Plugins: handling of unicode-characters is now correct.
15. Add mapping function: getdecimal(). Returns a python decimal; if not
    found or non-valid input: returns decimal 0.
16. For csv and fixed with 'noBOTSID': nextmessageblock can check for
    multiple fields, eg: nextmessageblock =
    ([{'BOTSID':'lin','field1':None},{'BOTSID':'lin','field2':None}])
17. When deleting configuration items via 'bulk delete': make a backup
    plugin first.

Bug fixes
~~~~~~~~~

1. There was a missing import in xml2botsgrammar
2. Logging of mapping debug did not work in 3.0
3. Correct handling of resends/rereceives for already resend/received
   files
4. Fixed bug in automaticretrycommunication
5. Confirmation can now be asked via channel-rule.
6. if multiple commands in run: reports etc are based on timestamp. This
   messed up the relation between runs and eg incoming files.

