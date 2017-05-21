## Isolated acceptance testing (bots\>=3.0)

This is a 'mode' for testing which is **isolated**: 

-	no external communication: all
	I/O is from/to file system 
-	system state does not change (eg no
	increased counters, no test runs in system, etc) Idea is to run an
	acceptance test without affecting your system (or the system of your
	edi-partner). 
    
**Note**: all plugins since 20130101 are suited for
isolated acceptances tests.

### Advantages

1.  Isolated acceptance tests are 'repeatable' (because same counters
    are used, same time is used etc). This is great for testing: each
    run of a test gives the same results. This makes it easy to compared
    the results automatically.
2.  By using isolated acceptance tests your test-environment can be
    equal to production-environment. So you can use standard directory
    comparison tools to push changes test-\>production.
3.  As the acceptance tests are isolated, this means an acceptance test
    can be run in a production-environment without affecting this
    environment. This way you can verify that after a change, all still
    runs as before in your production environment.


### Running isolated acceptance tests

1.  in all channels set 'testpath'. Testpath should point to a directory
    with test-files.
2.  Set option 'runacceptancetest' in bots.ini to 'True'.
3.  Run 'new'
4.  Check results of run with what you expect
5.  Delete runs/files from acceptance test (menu:Systasks-\>Bulk delete;
    select **only** 'Delete transactions in acceptance testing'.)


### Acceptance tests in plugins

Plugins since 20130101 can be run as acceptance tests.  
About the plugins with build-in acceptance test:

-   'testpath' for incoming files are in botssys\\infile
-   'testpath' for outgoing files go to botssys\\outfile
-   each plugin also contains the the expected outgoing files
    (botssys\\infile\\outfile); these are used to compare the results.
-   included is a route script
    (bots/usersys/routescripts/bots\_acceptancetest.py):
    -   before run: discard directory 'botssys\\outfile'.
    -   after run: global run results are compared with expectation
        (\#in, \#out. \#errors, etc)
    -   after run: compare files in botssys\\outfile with expected files
        in botssys\\infile\\outfile
    -   the output of these comparisons can be seen in terminal
        ('dos-box')


### Implementation Details

What bots does when running an isolated acceptance test:

-   channel-type is set to 'file'.
-   channel-path is set to the value in 'testpath'. if testpath is
    empty: use path.
-   channel-remove is set to 'off': no deletion of incoming files.
-   error-email: not send.
-   fixed date/time in envelopes and in mappings (if function
    transform.strftime() is used)
-   counters/references: fixed; counters are not incremented
-   incoming files are always read in same order.
-   outgoing-filename options: date/time is fixed
-   no archiving
-   additional user exits are run. User exits are in file
    usersys/routescripts/botsacceptancetest.py :
    -   before run:: function pretest. use eg to empty out-directories
        etc
    -   after run: function post-test. This can be used to check
        results, compare files etc
         After running an isolated acceptance test, the
        reports/filereports/data-files/etc generated during
        acceptance-testing can be deleted via: menu:Systasks-\>Bulk
        delete; select **only** 'Delete transactions in acceptance
        testing'.

Implementation remarks:

-	GUI does not have the results of post-test script (runs after
	automaticmaintanance); view this in terminal/dos-box.

-	communication scripts: script should check explicitly if in acceptance
	test and act accordingly.

-	database communication: script should check explicitly if in acceptance
	test and act accordingly.

