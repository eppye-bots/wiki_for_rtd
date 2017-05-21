Note: the [tutorial](StartMyFirstPlugin.md) contains some detailed
information and screen-shots of bots-monitor!

## Menu in bots-monitor

1.  Home: start page and general information.
2.  Last run: view results of the last run:
    -   incoming: view incoming files and results
    -   document: view status of business document. An edi file can
        contain multiple documents (eg orders). In this view are the
        results of the separate business documents. See [setting
        document views](ConfigurationBotskey.md)
    -   outgoing: view outgoing files and results
    -   process errors: view process errors; mostly these will be
        communication errors.
3.  All runs: view results of all runs:
    -   reports: view of all runs and results
    -   incoming: view incoming files and results
    -   document: view status of business document. An edi file can
        contain multiple documents (eg orders). In this view are the
        results of the separate business documents. See [setting
        document views](ConfigurationBotskey.md)
    -   outgoing: view outgoing files and results
    -   process errors: view process errors; mostly these will be
        communication errors.
    -   confirmations: view the results of confirmations you wanted and
        confirmation you gave. See [setup
        confirmations](Confirmations.md)
4.  Select: use criteria like date/time to view results you want to see
    like eg editype edifact or x12.
    -   Note: select screens can also be used using 'select' button in
        other views.
5.  Configuration: configuration of the edi setup.
6.  System tasks (administrators only): read plugins, create plugins,
    maintain users, etc.
7.  Run: manually start a run of bots-engine:
    -   Run (only new): receive, translate, and send new edi messages.
    -   Run userindicated rerecieves: receive previously received
        edi-files again from archive. User has to mark edi-files as
        're-receive' via incoming view.
    -   Run userindicated resends: resend previously send edi-files
        again. User has to mark edi-files as 're-send' via outgoing
        view.


### User interface tips

-	View screens often have a star at the beginning of each line; moving
	over the star will show possible actions.
-	In view screens, you can see the contents of an edi file if you click on
	the file name.
-	When viewing the contents of an edi file, you can go backwards and
	forwards to see the processing steps of the file.
-	Might be handy to use tabbed browsing.
-	Bots uses user rights (viewers, administrators and superuser). See
	[setting user rights](UserSecurity.md)

