Multiple Environments (bots>=2.1)
---------------------------------

There is more than one way of configuring multiple environments.
Directories relevant for separate environments are:

.. raw:: html

   <ul><li>

bots/config: global configuration; eg values for usersys, botssys,
database connection, port number.

.. raw:: html

   </li><li>

bots/botssys: storage of edi files, database, loggings etc.

.. raw:: html

   </li><li>

bots/usersys: grammars, mappings, route scripts etc.

.. raw:: html

   </li></ul>

.. raw:: html

   <h3>

1. Use config parameter

   .. raw:: html

      </h3>

Each bots program "start script" accepts a parameter (-c) that indicates
which config directory to use. Within config there are settings for
botssys and usersys, so this gives us the ability to have separate
environments. The default, if this parameter is not used, is config. By
example:

.. raw:: html

   <ol><li>

Start with configuration with the default config, usersys and botssys
directories in bots directory.

.. raw:: html

   </li><li>

Purpose is to create a 2nd environment (env2).

.. raw:: html

   </li><li>

Make copies of 3 directories within bots directory. Advised is to use
the same name-suffix:

.. raw:: html

   <ul><li>

Make copy of config, name it config-env2

.. raw:: html

   </li><li>

Make copy of botssys, name it botssys-env2

.. raw:: html

   </li><li>

Make copy of usersys, name it usersys-env2

.. raw:: html

   </li></ul></li><li>

Edit the configuration files in config-env2 and change (at least) the
following settings:

.. raw:: html

   <ul><li>

in bots.ini

.. raw:: html

   <pre><code> botssys = botssys-env2<br>
    usersys = usersys-env2 <br>
   </code></pre>
   </li><li>

settings.py

.. raw:: html

   <pre><code>DATABASE_NAME = os.path.join(PROJECT_PATH, 'botssys-env2/sqlitedb/botsdb')<br>
   </code></pre>
   </li></ul></li><li>

Start bots scripts using the -c parameter to refer to the new
environment, eg:

.. raw:: html

   <pre><code>bots-webserver.py -cconfig-env2<br>
   bots-engine.py -cconfig-env2<br>
   </code></pre>

Note: on linux the use of symlinks in bots directory might be useful.

.. raw:: html

   </li></ol>

.. raw:: html

   <h3>

2. Use different computers

   .. raw:: html

      </h3>

   Your production environment is on a server. Your development
   environment is on your desktop/laptop PC. In this way, you can
   replicate exactly the same setup (same python version etc), and
   transfer things from one to the other once tested.

.. raw:: html

   <h3>

3. Using different python installations

   .. raw:: html

      </h3>

   I used this for a long time for windows. I had python2.5 and 2.6
   installed; Bots in python 2.6 was my development environment; bots in
   python 2.5 was production. This is a very simple way to have 2
   environments in windows.

   .. raw:: html

      <h3>

   4. Using python virtualenv tool

      .. raw:: html

         </h3>

      virtualenv is a tool to create isolated Python environments. Each
      environment has a separate installation of bots and its
      dependencies, so different versions can be tested. You can
      activate and deactivate the environments as needed. You can use in
      combination with method 1 to have "config environments within
      python environments". Mike has just started testing this method
      and will add details soon...


