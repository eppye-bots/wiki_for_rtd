## Multiple Environments (bots\>=2.1) 

There is more than one way of configuring multiple environments.
 Directories relevant for separate environments are:

-   *bots/config*: global configuration; eg values for usersys, botssys,
    database connection, port number.
-   *bots/botssys*: storage of edi files, database, loggings etc.
-   *bots/usersys*: grammars, mappings, route scripts etc.


### 1. Use config parameter

Each bots program "start script" accepts a parameter (-c) that indicates
which config directory to use. Within config there are settings for
botssys and usersys, so this gives us the ability to have separate
environments. The default, if this parameter is not used, is
**config**.

 **By example:**

1.  Start with configuration with the default *config*, *usersys* and
    *botssys* directories in bots directory.
2.  Purpose is to create a 2nd environment (env2).
3.  Make copies of 3 directories within bots directory. Advised is to
    use the same name-suffix:
    -   Make copy of *config*, name it *config-env2*
    -   Make copy of *botssys*, name it *botssys-env2*
    -   Make copy of *usersys*, name it *usersys-env2*

4.  Edit the configuration files in *config-env2* and change (at least)
    the following settings:
    -   in bots.ini

             botssys = botssys-env2
             usersys = usersys-env2 

    -   settings.py

            DATABASE_NAME = os.path.join(PROJECT_PATH, 'botssys-env2/sqlitedb/botsdb')

5.  Start bots scripts using the -c parameter to refer to the new
    environment, eg:

        bots-webserver.py -cconfig-env2
        bots-engine.py -cconfig-env2

    Note: on linux the use of symlinks in bots directory might be
    useful.


### 2. Use different computers

Your production environment is on a server.  
Your development environment is on your desktop/laptop PC.  
In this way, you can replicate exactly the same setup (same python
version etc), and transfer things from one to the other once tested.


### 3. Using different python installations

I used this for a long time for windows.  
I had python2.5 and 2.6 installed;  
Bots in python 2.6 was my development environment; bots in python 2.5
was production.  
This is a very simple way to have 2 environments in windows.


### 4. Using python virtualenv tool

[virtualenv](https://pypi.python.org/pypi/virtualenv) is a tool to
create isolated Python environments.  
Each environment has a separate installation of bots and its
dependencies, so **different versions** can be tested. You can activate
and deactivate the environments as needed. You can use in combination
with method 1 to have "config environments within python environments".

Mike has just started testing this method and will add
[details](DeploymentMultipleEnvironmentsVirtual.md) soon...

