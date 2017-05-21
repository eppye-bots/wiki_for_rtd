## Options for running bots-engine

1.	Run automatic or manual 
	- 	Manual runs by using the 'run' options in the menu. 
    -	[Schedule](DeploymentEngine.md) 
    -	Use the [directory monitor/watcher](DirMonitor.md) 
    -	This can be combined; eg 
    	-	schedule 'new' every 15minutes 
        -	manually 'rereceive' and 'resend' 
        
1. 	Direct or via [jobqueue-server](Jobqueue.md) 
1. 	Specify the routes to run: 
	-	Run all routes. Default way of running (nothing specified). 
    -	Run all routes with excludes. Indicate in route if routes ought not to 
    	run in a default run. 
    -	Run specific routes: include route as parameters. Eg
		(command-line):
 		` bots-engine.py myroute1 myroute2 `
        
		Run **new or other**:
        
		-	new. Via run-menu or command-line:  
				` bots-engine.py --new`
		-	rereceive: rereceive user indicated edi files. Via run-menu or
			command-line:  
 				` bots-engine.py --rereceive`
		-	resend: resend user indicated edi-files. Via run-menu or command-line:  
        		` bots-engine.py --resend`
		-	automaticretrycommunication: resend edi-files where out-communication
			failed. Command-line:  
 				` bots-engine.py --automaticretrycommunication`
