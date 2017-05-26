Start FAQ
---------

**When starting bots-webserver the window disappears after a few seconds?**
    Start the bots-webserver from the command line; 
    you will be able to see what goes wrong. 
    (Windows, python 2.7) go to command line and: ``c:\python27\python c:\python27\Scripts\bots-webserver.py``
    For the most common cause for the problem see the next question.

**Bots-webserver gives error: IOError: Port 8080 not free on 'x.x.x.x' (or similar).**
    | Another program already uses this 'port'.
    | Adapt the port bots uses: in configuration file bots/config/bots.ini look for 'port'.
    | Change port to eg 8090
    | Start bots-webserver again.
    | In your browser you will have to indicate another port eg: http://localhost:8090

**Can I run multiple instances of bots-engine in parallel?**
    | No, this is not possible.
    | Instead bots >= 3.0 has better control of running the engine: :ref:`jobqueue server <job-queue-server>`.
