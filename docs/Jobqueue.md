## Bots Job Queue (bots \>= 3.0)

Purpose of the bots jobqueue is to enable better scheduling of bots engine: 

-	ensures only a single bots-engine runs at any time. 
-	no engine runs are lost/discarded.
-	next engine run is started as soon as previous run has ended. Use of the
	job queue is optional, but is recommended if [scheduling bots-engine](DeploymentEngine.md).

Details: 

- 	Launch sequence from the queue can be controlled using
	different priorities when adding jobs. 
-	Other (non bots-engine) jobs can also be added to the queue if they need 
	to be run "in between" 	bots-engine runs. 
-	If you add a duplicate of another job \_already
	waiting on the queue\_ the request is discarded. This is because the job
	on the queue will perform the same action when it runs. If that job is
	already running, the new job \_will\_ be added to the queue. 
-	logging in \_bots/botssys/logging/jobqueue.log\_ 
-	When using Bots monitor run-menu the job queue will be used if enabled in 
	bots.ini; jobs are added with default priority of 5. 
-	In production you'll probably want  to run bots-jobqueueserver as a 
	[daemon process/service](DaemonProcesses.md). 
-	Full command-line usage instructions for bots-job2queue.py and 
	bots-jobqueueserver.py when started up with '--help' 
-	The bots job queue server does 3 things 
	-	maintains a queue of jobs for bots-engine. 
    - 	receives new jobs via the bots-job2queue.py 
    	(or via \_bots-monitor-\>Run\_) 
    -	launches a new job from the queue as soon as previous job ended.

### Starting with the job queue

1.  First, enabled in [bots.ini](StartConfigurationFiles.md) (jobqueue
    section, enabled = True).
2.  Start the bots-jobqueueserver. Command-line:
    ` bots-jobqueueserver.py `
3.  Put jobs in the job queue:
    -   via menu using *bots-monitor-\>Run*
    -   start from command-line (using bots-job2queue.py).
    -   start from scheduler (using bots-job2queue.py).


### Command examples

Job2queue on windows example 1:

    c:\python27\python c:\python27\Scripts\bots-job2queue.py c:\python27\python c:\python27\Scripts\bots-engine.py

Job2queue on windows example 2:

    c:\python27\python c:\python27\Scripts\bots-job2queue.py -p3 c:\python27\python c:\python27\Scripts\bots-engine.py --new -Cconfigprod

Job2queue on windows example 3 (Adding other commands to the job queue):

    c:\python27\python c:\python27\Scripts\bots-job2queue.py c:\program files\my_program.exe my_parm_1 my_parm_2

Job2queue on linux example 4:

    bots-job2queue.py bots-engine.py

Job2queue on linux example 5:

    bots-job2queue.py -p3 bots-engine.py --new -Cconfigprod
