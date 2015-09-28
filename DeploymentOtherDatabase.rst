Use MySQL or PostgreSQL as database
===================================

Backgrond information: \* Default bots uses a SQLite database. This is
included in the standard installation and works out-of-the-box.
Performance of SQLite is good! \* Bots always uses utf-8 in the database
communication. \* Database tables are installed using django-machinery.
See django docs. \* After installation, you may want to `migrate some
data <MigrateDatabase.md>`__. \* You might have to manually add a
database trigger if using `persist functions <MappingPersist.md>`__.

.. raw:: html

   <h2>

PostgreSQL

.. raw:: html

   </h2>
   <ol><li>

install PostgreSQL.

.. raw:: html

   </li><li>

install psycopg2 as python database adapter.

.. raw:: html

   </li><li>

login in command line client of database.

.. raw:: html

   </li><li>

Create database (CLI) : CREATE DATABASE botsdb WITH ENCODING 'UTF8';

.. raw:: html

   </li><li>

Create user (CLI): CREATE USER bots WITH PASSWORD 'botsbots';

.. raw:: html

   </li><li>

Give user rights: (CLI) GRANT ALL PRIVILEGES ON DATABASE botsdb TO bots;

.. raw:: html

   </li><li>

make sure database accepts connections over (non-local) TCP/IP: change
parameter listen\_addresses in in postgresql.conf; add/change setting
for user in pg\_hba.conf.

.. raw:: html

   </li><li>

Set connection parameter in bots configuration in
bots/config/settings.py. Examples are provided - see comments in
settings.py

.. raw:: html

   </li><li>

Create the required tables (CLI):

.. raw:: html

   <ul><li>

(CLI)  django-admin syncdb --settings='bots.config.settings'

      .. raw:: html

         </li><li>

      (CLI) or when bots is not installed in the default directory:
            django-admin syncdb --pythonpath='path to bots'
            --settings='bots.config.settings'

            .. raw:: html

               </li><li>

            Django asks for name etc of default user.

            .. raw:: html

               </li></ul></li></ol>

.. raw:: html

   <h2>

MySQL

.. raw:: html

   </h2>
   <ol><li>

install MySQL.

.. raw:: html

   </li><li>

install mysql-Python as python database adapter.

.. raw:: html

   </li><li>

login in command line client of database.

.. raw:: html

   </li><li>

Create database (CLI): CREATE DATABASE botsdb DEFAULT CHARSET utf8;

.. raw:: html

   </li><li>

Create user (CLI): CREATE USER 'bots' IDENTIFIED BY 'botsbots';

.. raw:: html

   </li><li>

Give user rights (CLI): GRANT ALL PRIVILEGES ON botsdb.\* TO 'bots';

.. raw:: html

   </li><li>

make sure database accepts connections over (non-local) TCP/IP: change
parameter 'binds' in /etc/mysql/my.cfg.

.. raw:: html

   </li><li>

Set connection parameter in bots configuration in
bots/config/settings.py. Examples are provided - see comments in
settings.py

.. raw:: html

   </li><li>

Create the required tables:

.. raw:: html

   <ul><li>

(CLI)  django-admin syncdb --settings='bots.config.settings'

      .. raw:: html

         </li><li>

      (CLI) or when bots is not installed in the default directory:
            django-admin syncdb --pythonpath='path to bots'
            --settings='bots.config.settings'

            .. raw:: html

               </li><li>

            Django asks for name etc of default user.

            .. raw:: html

               </li></ul></li></ol>

.. raw:: html

   <h2>

MySQL on Windows

.. raw:: html

   </h2>
   <ol><li>

Download MySQL community server msi installer. (tested version 5.5.20)

.. raw:: html

   </li><li>

Run the installer, do a "typical" installation and follow the prompts.
On the final screen, make sure Launch the MySQL Instance Configuration
Wizard box is ticked.

.. raw:: html

   </li><li>

When the configuration wizard starts, make the following selections:

.. raw:: html

   <ul><li>

Detailed configuration

.. raw:: html

   </li><li>

Server machine (you may choose developer for your bots test environment)

.. raw:: html

   </li><li>

Transactional database

.. raw:: html

   </li><li>

DSS/OLAP (20 connections)

.. raw:: html

   </li><li>

Enable TCP/IP and Strict mode (defaults)

.. raw:: html

   </li><li>

Best support for multilingualism (UTF8)

.. raw:: html

   </li><li>

Install as Windows service (default)

.. raw:: html

   </li><li>

Modify security settings; enter a root password and write it down.

.. raw:: html

   </li><li>

Execute configuration

.. raw:: html

   </li><li>

Create a shortcut to C:FilesServer 5.5.exe in case you want to modify
any of these settings later.

.. raw:: html

   </li></ul></li><li>

Go to Start > Programs > MySQL > MySQL Server > MySQL Command Line
Client. Enter your root password when prompted. You should now have a
mysql> command prompt.

.. raw:: html

   </li><li>

Enter the following MySQL commands at the prompt:

.. raw:: html

   <pre><code>mysql&gt; CREATE DATABASE botsdb DEFAULT CHARSET utf8;<br>
    Query OK, 1 row affected (0.01 sec)<br>
   <br>
   mysql&gt; CREATE USER 'bots' IDENTIFIED BY 'botsbots';<br>
    Query OK, 0 rows affected (0.00 sec)<br>
   <br>
   mysql&gt; GRANT ALL ON botsdb.* TO 'bots';<br>
    Query OK, 0 rows affected (0.03 sec)<br>
   <br>
   </code></pre>
   </li><li>

Download and install MySQL-python for Windows to suit your python
version (tested MySQL-python-1.2.3.win32-py2.7.exe)

.. raw:: html

   </li><li>

Set connection parameters in bots configuration in
bots/config/settings.py. MySQL example is provided, I only changed HOST.

.. raw:: html

   <pre><code>#MySQL:<br>
   DATABASES = {<br>
       'default': {<br>
           'ENGINE': 'django.db.backends.mysql',<br>
           'NAME': 'botsdb',<br>
           'USER': 'bots',<br>
           'PASSWORD': 'botsbots',<br>
           'HOST': 'localhost',  #database is on same server as Bots<br>
           'PORT': '3306',<br>
           'OPTIONS': {'use_unicode':True,'charset':'utf8','init_command': 'SET storage_engine=INNODB'},<br>
           }<br>
       }<br>
   </code></pre>
   </li><li>

Create the required tables from a command prompt. Django asks for name
etc of superuser. (enter user: bots, password: botsbots)

.. raw:: html

   <pre><code>&gt; D:\python27\python.exe D:\Python27\lib\site-packages\django\bin\django-admin.py syncdb <br>
     --settings=bots.config.settings<br>
   <br>
   Creating tables ...<br>
   Creating table auth_permission<br>
   Creating table auth_group_permissions<br>
   Creating table auth_group<br>
   Creating table auth_user_user_permissions<br>
   Creating table auth_user_groups<br>
   Creating table auth_user<br>
   Creating table auth_message<br>
   Creating table django_content_type<br>
   Creating table django_session<br>
   Creating table django_admin_log<br>
   Creating table confirmrule<br>
   Creating table ccodetrigger<br>
   Creating table ccode<br>
   Creating table channel<br>
   Creating table partnergroup<br>
   Creating table partner<br>
   Creating table chanpar<br>
   Creating table translate<br>
   Creating table routes<br>
   Creating table filereport<br>
   Creating table mutex<br>
   Creating table persist<br>
   Creating table report<br>
   Creating table ta<br>
   Creating table uniek<br>
   <br>
   You just installed Django's auth system, which means you don't have any superusers defined.<br>
   Would you like to create one now? (yes/no): yes<br>
   Username (Leave blank to use 'mike'): bots<br>
   E-mail address: bots@bots.com<br>
   Password: botsbots<br>
   Password (again): botsbots<br>
   Superuser created successfully.<br>
   Installing custom SQL ...<br>
   Installing indexes ...<br>
   No fixtures found.<br>
   </code></pre>
   </li><li>

Now start bots-webserver and log in as bots.

.. raw:: html

   </li></ol>

Note: The database is stored in C:/ProgramData/MySQL/MySQL Server
5.5/Data/ by default (on Windows 7). To move the database, do the
following:

.. raw:: html

   <ol><li>

Stop the MySQL service

.. raw:: html

   </li><li>

Move the /Data/ folder only to your required location (eg. D:/MySQL
Server 5.5/Data/

.. raw:: html

   </li><li>

Make sure the permissions are moved with it. "NETWORK SERVCE" must have
full control

.. raw:: html

   </li><li>

Change the setting "datadir" in C:/ProgramData/MySQL/MySQL Server
5.5/my.ini to indicate the new folder location

.. raw:: html

   <pre><code># Path to the database root<br>
   datadir=D:/MySQL Server 5.6/Data<br>
   </code></pre>
   </li><li>

Restart the MySQL service. If it will not start, check permissions!
