## Return codes for bots engine (bots>=3.0) ##

Bots-engine uses the following return codes:

-	0: OK, no errors.
-	1: (system) errors: could not connect to database, not correct command line arguments,  database damaged, unexpected system error etc.
-	2: bots ran OK, but there are errors/process errors in the run.
-	3: Database is locked, but "maxruntime" has not been exceeded. (use the job queue server to avoid this type of errors).


Return code '2' is similar/equivalent to the error reports by email.