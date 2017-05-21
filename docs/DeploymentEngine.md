## Scheduling introduction

-   Bots does not have a built-in scheduler. Scheduling is done by the scheduler of your OS. 
    -   Windows: use eg [Windows Task Scheduler](http://support.microsoft.com/kb/308569).
    -   Linux/unix: use eg [cron](http://www.linuxhelp.net/guides/cron/).


-   Bots-engine does not run concurrently (in parallel). If a previous
    run is still in progress, a new run will not start. From version 3.0
    onwards, Bots includes an optional [job queue server](Jobqueue.md)
    to use when scheduling Bots engine. Using this is recommended, to
    prevent discarding runs that overlap.
-   Strong advice: when scheduling bots-engine, activate the sending of
    automatic [email-reports for errors](DeploymentErrorReports.md).


### Possible scheduling scenarios

(command lines below are for Windows):

-   If all (or most) routes can be run on the same schedule, then just
    schedule bots-engine "new" run as often as you need, Eg. every 5
    minutes. To exclude some routes from this run, tick the
    *Notindefaultrun* box in the route advanced settings. These can then
    be scheduled separately by specifying route names on the command
    line.

        c:\python27\python c:\python27\Scripts\bots-engine.py --new

        c:\python27\python c:\python27\Scripts\bots-engine.py "my hourly route"

-   If you have few routes but with varying schedules, then schedule
    them individually (by putting route names on the command line).
    Disadvantage: newly added routes are not automatically run, you must
    adjust your schedule.

        c:\python27\python c:\python27\Scripts\bots-engine.py "my orders route" "my invoice route"

        c:\python27\python c:\python27\Scripts\bots-engine.py "my daily route"

-   Consider whether you need to schedule retries periodically.
    Particularly with accessing remote servers, sometimes there may be
    communication errors that would be ok next time bots tries.
    Otherwise you will need to retry these yourself. File errors are not
    retried automatically because the same error will just come up
    again!

        c:\python27\python c:\python27\Scripts\bots-engine.py --automaticretrycommunication


### My Setup (Mike)

I am using Windows task scheduler and Bots [job queue](Jobqueue.md) is
enabled. I have five scheduled tasks:

1.  Bots-engine (every 5 minutes, 24x7)
2.  Bots-engine-hourly (every hour on the hour)
3.  Bots-engine-daily (1am daily)
4.  Bots-engine-weekly (1am every Monday morning)
5.  Bots-engine-monthly (1am first of the month)
    Each task has a corresponding batch file in the scripts directory. This
    makes task configuration and changes easier; the scheduled tasks simply
    call the batch files. Within the batch files I use job2queue.py for
    adding jobs. Some add only a single job, while some add multiple jobs.
    (You could also put the command lines directly into Windows task
    scheduler, each one as a separate task). I use appropriate priorities
    for each job, as some times of the day Bots can get very busy. Several
    examples are shown below.
    
        :: bots-engine.bat
        :: Regular run of bots engine (eg. every 5 minutes, highest priority)
        C:\python27\python.exe C:\python27\scripts\bots-job2queue.py -p1 C:\python27\python.exe C:\python27\scripts\bots-engine.py --new
        
        :: bots-engine-hourly.bat

        :: Hourly monitoring alerts
        C:\python27\python.exe C:\python27\scripts\bots-job2queue.py -p2 C:\python27\python.exe C:\python27\scripts\bots-engine.py hourly_alerts

        :: Hourly cleanup and low priority routes
        C:\python27\python.exe C:\python27\scripts\bots-job2queue.py -p6 C:\python27\python.exe C:\python27\scripts\bots-engine.py ftp_cleanup ProductionOrders RemitAdvice

        :: automatic retry of failed outgoing communication
        C:\python27\python.exe C:\python27\scripts\bots-job2queue.py -p7 C:\python27\python.exe C:\python27\scripts\bots-engine.py --automaticretrycommunication

        :: bots-engine-daily.bat
        
        :: daily housekeeping
        C:\python27\python.exe C:\python27\scripts\bots-job2queue.py -p3 C:\python27\python.exe C:\python27\scripts\bots-engine.py daily_housekeeping

        :: daily reporting & SAP data downloads
        C:\python27\python.exe C:\python27\scripts\bots-job2queue.py -p9 C:\python27\python.exe C:\python27\scripts\bots-engine.py daily_reports SAP_Expired_Contracts
