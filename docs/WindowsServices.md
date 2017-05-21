## Creating Windows Services 

If running Bots on a Windows server, you
can create services to keep the important background processes running.
This is the equivalent of a "daemon" process in Linux. 

### Prerequisites  
-   **srvany.exe** - This is a Microsoft utility
    included in the Windows Server [Resource Kit
    Tools](http://www.microsoft.com/download/en/details.aspx?id=17657). 
-   **sc.exe** -
    The SC command is included by default in most Windows installations and
    is also available in the resource kit. 
-   Python and Bots are already
    installed and working, of course! 
    
### Procedure
-   Copy srvany.exe to C:\\Windows\\System32 
-   Open a command prompt and enter
    the following commands, according to the service required. Note:
    position of equal signs and spaces must be exactly as shown. 
    ``` sc create "Bots Webserver" binPath= "C:\\Windows\\System32\\srvany.exe"
        start= auto DisplayName= "Bots Webserver" sc description "Bots
        Webserver" "This is the webserver for Bots EDI translator." 
    ```
    ``` sc create "Bots Job Queue" binPath=
        "C:\\Windows\\System32\\srvany.exe" start= auto DisplayName= "Bots Job
        Queue" sc description "Bots Job Queue" "Provides job queue and launch
        functionality for Bots EDI Translator" 
    ``` 
    ``` sc create "Bots Directory Monitor" binPath= "C:\\Windows\\System32\\srvany.exe" start=
        auto DisplayName= "Bots Directory Monitor" sc description "Bots
        Directory Monitor" "Monitors one or more directories for new files and
        creates Bots jobs to process them" 
    ``` 
-   Run regedit and navigate to
    \`HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\\` 
-   In the right hand pane of regedit, right click, New, Key, call it
    \`Parameters\`. 
-   Click the new Parameters key to select it. 
-   In the right hand pane, right click, New, String value, call it
    \`Application\`. 
-   Double click Application, enter the command to run
    the required Bots script. This will vary according to your installed
    location and Bots version, eg. 
    ``` C:\\Python27\\python.exe
        C:\\Python27\\Scripts\\bots-webserver.py 
        C:\\Python27\\python.exe C:\\Python27\\Scripts\\bots-jobqueueserver.py 
        C:\\Python27\\python.exe C:\\Python27\\Scripts\\bots-dirmonitor.py 
     ``` 
-   Run \`services.msc\`
    to start/stop/configure your new services. 
    
### Reference links
-   <http://support.microsoft.com/?kbid=137890>
-   <http://support.microsoft.com/?kbid=251192>

------------------------------------------------------------------------

If any of the above doesn't make sense to you, I have created a small
free utility program to do it all. This is a general purpose program for
creating services. My service configuration for Bots is included; you
may need to edit the paths to suit your installation. You can download
the program from
[here](https://dl.dropboxusercontent.com/u/43043107/CreateWinSrv.zip).


[![](https://dl.dropboxusercontent.com/u/43043107/CreateWinSrv1.png)](https://dl.dropboxusercontent.com/u/43043107/CreateWinSrv.zip)

