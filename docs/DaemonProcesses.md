# Run as service/daemon #

_A [daemon](http://en.wikipedia.org/wiki/Daemon_%28computing%29) is a computer program that runs continuously as a background process._

After Bots installation there are no service/daemon processes active. This is recommended for a production environment. Bots has several parts that you may want to run as services/daemons:

-	bots-webserver.py
-	bots-jobqueueserver.py (bots >= 3.0.0, is optional)
-	bots-dirmonitor.py (bots >= 3.0.0, is optional)

Note that bots-engine itself is not a daemon process; bots-engine is best [scheduled](DeploymentEngine.md).

How these daemons are created and managed depends on the operating system being used:

-	In Windows, you can set them up as [Windows Services](WindowsServices.md).
-	In linux/unix, you can start them as [Linux daemons](LinuxDaemons.md).