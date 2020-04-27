Multiple Environments
=====================

There are several ways to configure multiple seperate environments for bots.


Using python virtualenv tool
----------------------------

    * Virtualenv is a tool to create isolated Python environments. Virtualenv creates a folder which contains all the necessary executables to use the packages that a Python project would need.
    * Bots works fine using virtualenv.
    * Installation for linux is similar to a normal install. See `Installation <installation>`
    * Installation for windows: use a pip install, see `Installation <installation>`
    * Please google for virtualenv instructions.


Use config parameter
--------------------

    Each bots program *start script* accepts a parameter (-c) that indicates which config directory to use. Within config there are settings for botssys and usersys, so this gives us the ability to have separate environments..

    #. Start with configuration with the default ``config``, ``usersys`` and ``botssys`` directories in bots directory.
    #. Make copies of those directories within bots directory:
        * Make copy of ``config``, name it eg ``config-env2``
        * Make copy of ``botssys``, name it eg ``botssys-env2``
        * Make copy of ``usersys``, name it eg ``usersys-env2``
    #. Edit the configuration files in ``config-env2`` and change (at least) the following settings:
        * in bots.ini

            .. code::

                botssys = botssys-env2
                usersys = usersys-env2

        * settings.py

            ``DATABASE_NAME = os.path.join(PROJECT_PATH, 'botssys-env2/sqlitedb/botsdb')``

    #. Start bots scripts using the -c parameter to refer to the new environment, eg:

        .. code:: console

            $ bots-webserver.py -cconfig-env2
            $ bots-engine.py -cconfig-env2


Different computers
-----------------------

    * Your production environment is on a server.
    * Your development environment is on your desktop/laptop PC.
    * In this way, you can replicate exactly the same setup (same python version etc), and transfer things from one to the other once tested.



Addition tweaks to run multiple Bots environments at same time
--------------------------------------------------------------

   *bots.ini*

    .. code:: python

        [settings]
        #port used to assure only one instance of bots-engine is running. default: 28081
        port = 28091

        [webserver]
        #port at which at bots-gui is server. default is 8080
        port = 8090

        [jobqueue]
        # Port to use for the job queue xmlrpc server (on localhost). Default: 28082
        port = 28092


    *settings.py*

    .. code:: python

        SESSION_COOKIE_NAME = 'bots310'
        SECRET_KEY = 'm@-u37qiujmeqfbu$daaaaz)sp^7an4u@h=wfx9dd$$$zl2i*x9#awojdc'
