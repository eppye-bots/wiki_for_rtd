## List of Changes

### Wrapping of user script functionality into GUI

-   For outgoing filenames: can include partnerID, messagetype, botskey, data/time, etc in channel.
-   Pass-through is option in route.
-   Zip and unzip files as option in channel.
-   SSL keyfile and certificate as options in channel.
-   Excel as incoming messagetype (instead of via preprocessing).
-   Option in channel to indicate edi file in email should be in body.
-   Add: communication-out type 'trash' to discard of edi files.

### Improved 'run' options
-   Run options in GUI are simpler: new, rereceive, resend. (Automatic recommunication is possible via bots-engine).
-   Communication errors are visible in outgoing-screen and can be 'resend' manually.
-   Add 'resend all' and 'rereceive all' in incoming/outgoing screen; espc. useful in combination with selections.
-   Indicate in screens a file has been resend; Keep track of number of resends of an outgoing file. Filer works 'over' resends now.
-   Dropped 'retry' option. This was not useful and confusing. Use 'rereceive'.
-   Dropped 'retry communication'. Use 'resend', easier and more consistent.
-   Add: use 'channel' in selects (eg useful for resend selects).

### Better scheduling for bots-engine
-   Add: jobqueueserver. This makes complicated scheduling much better/easier; scheduled jobs will not be dropped anymore.
-   Add: directory-monitor: start engine when file is dropped in directory.
-   Cleanup runs only once a day now (in the first run of day); better performance.
-   Cleanup now also runs VACUUM for sqlite; better performance.
-   All edifact, x12, tradacoms files go via mailbag, x12. This is simpler. (there is a compatibility option in bots.ini).
-   Set max file-size in translations (value can be changed in bots.ini). Very big edi files take a long time to process.
-   Improve: engine now runs all routes if not new (unless routes have been specified as parameters).

### Configuration change management [see wiki](DeploymentEnv.md)
-   Use tools to push changes test-> production
    -   Via GUI: write database configuration to usersys in order to compare environments.
    -   Via GUI: read the changed database configuration in usersys after pushing changes
-   Isolated acceptation tests: run an acceptance test set without changes.
    -   option in bots.ini to active 'acceptance test'
    -   bots prevents communication to 'outside
    -   use seperate path to read/write ('testpath')
    -   do not change counters etc
    -   results of acceptance tests can be deleted/removed
    -   etc

### Many improvements in GUI, eg:
-   'Detail' screen has a better layout.
-   Improve: show name partner in selectlist (in configuration).
-   Improve: show channel-type in selectlist and routes (in configuration). I find this very convenient.
-   Improve: better sorting in configuration for in django 1.4, eg for routes, codelists, trasnlations.
-   References in a configuration are better guarded. Eg: when deleting partner that is used in partner-specific translation: user is warned, has to confirm.
-   Improve: removed charset from channel. This was not needed.
-   Improve: selections in screens not only for partners but also for partner groups
-   Fix: download an edi-file via filer could give not-correct file.
-   Add: keep track of file-size of incoming/outgoing files.

### Extended partner functionality
-   Add: function 'partnerlookup' for use in mapping scripts to look-up/convert partner related functions.
-   Add: extra partner fields: address, user-defined fields.
-   Add: send a message to any bots partner from mapping script (use partners as the email address book).
-   Improve: multiple email addresses in cc field.

### Confirmations
-   Fix: bug in confirmation logic for frompartner/topartner (I had them reversed...).
-   Better CONTRL-message.
-   Option to run user exit either to generate CONTRL message or change the generated CONTRL message.
-   messagetype (for incoming) is now similar to other uses of message-type; edi-type is removed (is not needed)
-   Fix: better indexing for reference/botskey. This improves performance for confirmations.

### Plugins
-   Always make configuration backup when reading new plugin.
-   Dropped the date-indication for files that are overwritten.
-   Index file in plugin always starts with type of plugin and layout is sorted/predictable.
-   Fix for performance problem when generating plugin for big plugins.
-   Fixed bug for relations in database. Bug only occurs when reading 'hand-changed'-plugins.

### Better handling of 'database is locked'/crash recovery
-   First of all: use the jobqueue-server for more complicated scheduling (prevents running multiple engine!)
-   Different way of detecting another instance of engine is running via locking of port.
-   If bots-engine finds no other engine is running, but the database is locked this indicates the previous run was ended unexpectedly (eg computer crash). In htis case bots will do an automatic 'crash recovery'. A warning is still given in logs or via email. Only ONE email is send.

### Technical
-   An 64-bits installer for windows is available.
-   Runs with django 1.4 now ; dropped support for django 1.1, 1.2
-   Database has changed. A script is added to upgrade the database.

### Other changes
-   Add: startup script for bots-webserver using apache. Multiple bots-environments can run over one apache server.
-   Add: user exit for cleanup.
-   Improve: use external file name in archive.
-   Add: archive as zip-files.
-   Fix: port was not used in initializing PostgreSQL.
-   Less statuses in processing (simpler, faster).
-   Improve: use unlimited text fields in database for errortext and persist.
-   Improve: if message in incoming edi file has error in mapping script and/or writing outgoing file: process rest of edi file (there is a compatibility option in bots.ini).
-   Reworked errors for edi files (parsing, generating). All errors have numbers now (for referencing).
-   Always read incoming files sorted by name. Reason: predictability. Formerly the read order was not predicable.
-   Fix: better handling of import errors for user scripts. This could lead to confusing errors/situations.
-   Add: access to whole envelope in mapping.
-   Fix: nr of messages was not used correctly when writing multiple UNH in one mapping script.
-   Fix: bug for numerical fields with more than 4 decimal positions.
-   Add: counter(s) per bots-run in mapping script; eg useful for UNH/ST counter per interchange.
-   Fix: enveloping for edifact with keca-character-set.
-   Add: concatenate function for usage in mapping scripts.
-   Improve: updated grammar-handling to allow for UNS-UNS construction.
-   Improve: set explicit namespace when generating xml.
-   Add: determine translation via user scripting.
-   Add: user scripts can easy detect what type of run is done via routedict['command']
-   Dropped: intercommit connector.
