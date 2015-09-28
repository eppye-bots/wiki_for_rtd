Bots Directory Monitor (bots >= 3.0)
------------------------------------

This provides a method of monitoring specific "local" directories, and
running Bots engine when files are ready to be processed.

Use of the directory monitor is optional. It may be useful for
processing files that only arrive occasionally and at random times.

Prerequisites
~~~~~~~~~~~~~

Directory monitor uses the `job queue <Jobqueue.md>`__. Monitoring must
be configured in bots.ini (dirmonitorX sections) Directory monitor
daemon process must be started (bots-dirmonitor.py)
