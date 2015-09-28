Scheduling introduction
-----------------------

-  Bots does not have a built-in scheduler. Scheduling is done by the
   scheduler of your OS.

   -  Windows: use eg `Windows Task
      Scheduler <http://support.microsoft.com/kb/308569>`__.

      .. raw:: html

         <ul><li>

      Linux/unix: use eg cron.

      .. raw:: html

         </li></ul><ul><li>

      Bots-engine does not run concurrently (in parallel). If a previous
      run is still in progress, a new run will not start. From version
      3.0 onwards, Bots includes an optional job queue server to use
      when scheduling Bots engine. Using this is recommended, to prevent
      discarding runs that overlap.

      .. raw:: html

         </li><li>

      Strong advice: when scheduling bots-engine, activate the sending
      of automatic email-reports for errors.

      .. raw:: html

         </li></ul>

.. raw:: html

   <h2>

Possible scheduling scenarios

.. raw:: html

   </h2>

(command lines below are for Windows):

.. raw:: html

   <ul><li>

If all (or most) routes can be run on the same schedule, then just
schedule bots-engine "new" run as often as you need, Eg. every 5
minutes. To exclude some routes from this run, tick the Notindefaultrun
box in the route advanced settings. These can then be scheduled
separately by specifying route names on the command line.

.. raw:: html

   <pre><code>c:\python27\python c:\python27\Scripts\bots-engine.py --new<br>
   </code></pre>
   <pre><code>c:\python27\python c:\python27\Scripts\bots-engine.py "my hourly route"<br>
   </code></pre>
   </li><li>

If you have few routes but with varying schedules, then schedule them
individually (by putting route names on the command line). Disadvantage:
newly added routes are not automatically run, you must adjust your
schedule.

.. raw:: html

   <pre><code>c:\python27\python c:\python27\Scripts\bots-engine.py "my orders route" "my invoice route"<br>
   </code></pre>
   <pre><code>c:\python27\python c:\python27\Scripts\bots-engine.py "my daily route"<br>
   </code></pre>
   </li><li>

Consider whether you need to schedule retries periodically. Particularly
with accessing remote servers, sometimes there may be communication
errors that would be ok next time bots tries. Otherwise you will need to
retry these yourself. File errors are not retried automatically because
the same error will just come up again!

.. raw:: html

   <pre><code>c:\python27\python c:\python27\Scripts\bots-engine.py --automaticretrycommunication<br>
   </code></pre></li></ul>

.. raw:: html

   <h3>

My Setup (Mike)

.. raw:: html

   </h3>

I am using Windows task scheduler and Bots job queue is enabled. I have
five scheduled tasks:

.. raw:: html

   <ol><li>

Bots-engine (every 5 minutes, 24x7)

.. raw:: html

   </li><li>

Bots-engine-hourly (every hour on the hour)

.. raw:: html

   </li><li>

Bots-engine-daily (1am daily)

.. raw:: html

   </li><li>

Bots-engine-weekly (1am every Monday morning)

.. raw:: html

   </li><li>

Bots-engine-monthly (1am first of the month) Each task has a
corresponding batch file in the scripts directory. This makes task
configuration and changes easier; the scheduled tasks simply call the
batch files. Within the batch files I use job2queue.py for adding jobs.
Some add only a single job, while some add multiple jobs. (You could
also put the command lines directly into Windows task scheduler, each
one as a separate task). I use appropriate priorities for each job, as
some times of the day Bots can get very busy. Several examples are shown
below.

.. raw:: html

   <pre><code>:: bots-engine.bat<br>
   <br>
   :: Regular run of bots engine (eg. every 5 minutes, highest priority)<br>
   C:\python27\python.exe C:\python27\scripts\bots-job2queue.py -p1 C:\python27\python.exe C:\python27\scripts\bots-engine.py --new<br>
   </code></pre>
   <pre><code>:: bots-engine-hourly.bat<br>
   <br>
   :: Hourly monitoring alerts<br>
   C:\python27\python.exe C:\python27\scripts\bots-job2queue.py -p2 C:\python27\python.exe C:\python27\scripts\bots-engine.py hourly_alerts<br>
   <br>
   :: Hourly cleanup and low priority routes<br>
   C:\python27\python.exe C:\python27\scripts\bots-job2queue.py -p6 C:\python27\python.exe C:\python27\scripts\bots-engine.py ftp_cleanup ProductionOrders RemitAdvice<br>
   <br>
   :: automatic retry of failed outgoing communication<br>
   C:\python27\python.exe C:\python27\scripts\bots-job2queue.py -p7 C:\python27\python.exe C:\python27\scripts\bots-engine.py --automaticretrycommunication<br>
   </code></pre>
   <pre><code>:: bots-engine-daily.bat<br>
   <br>
   :: daily housekeeping<br>
   C:\python27\python.exe C:\python27\scripts\bots-job2queue.py -p3 C:\python27\python.exe C:\python27\scripts\bots-engine.py daily_housekeeping<br>
   <br>
   :: daily reporting &amp; SAP data downloads<br>
   C:\python27\python.exe C:\python27\scripts\bots-job2queue.py -p9 C:\python27\python.exe C:\python27\scripts\bots-engine.py daily_reports SAP_Expired_Contracts<br>
   </code></pre>

