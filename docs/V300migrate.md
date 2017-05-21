## Migrate/update to 3.0.0

### Introduction

Version 3.0 is a bigger update for bots, view [all
changes](Migrate300.md\#List\_of\_Changes). 

Overview: 

1. 	Django 1.1 and 1.2 are not supported anymore. Supported are django 1.3 and 1.4. 
1.	Settings.py is changed. Advised: use the new settings.py, and do your
	customization in the new setting.py (eg for error reports, maybe
	database and timezone). 
1. 	The database has changed. A script is included to change the database. 
	I had no database issues while testing this migration. 
1. 	lots of changes in bots.ini. The 'old' bots.ini is
	OK, but it is advised to use new bots.ini, and do your customizations
	there. 
1. 	Excel input: does work; but is now an incoming messagetype and
	not via 'preprocessing'. 
1. 	Most user scripts will work; many user scripts are not needed anymore 
	because the functionality is provided by bots now. 
1. 	Some functions that may be used in user scripting have
	changed: 
    - 	botslib.change() -\> botslib.changeq(). This function is
		used to in processing incoming 997's and CONTRL!! 
    -	botsengine routescripts: for 'new' runs in routescript botsengine.py 
     	called function postnewrun(routestorun) -\> postnew(routestorun) 
    -	communication.run(idchannel,idroute) -\>
		communication.run(idchannel,command,idroute). Command is one of:
		'new','automaticretrycommunication','resend','rereceive'. 
    -	transform.run(idchannel,idroute) -\>
		transform.run(idchannel,command,idroute). Command is one of:
		'new','automaticretrycommunication','resend','rereceive'. My
		experiences: after changing settings.py and database migration, all
		works (except for and issues mentioned above).


### Summary of procedure

1.  make a backup!
2.  rename existing installation.
3.  do a fresh install.
4.  copy old data to new installation.
5.  change settings
6.  update the database.
     Comments:
7.  It is critical to change the settings before updating the database!
    Bots finds the right database via the settings!
8.  If you use MySQL or PostGreSQL: same procedure. The bots-updatedb
    script also updates MySQL or PostGreSQL.
9.  Tested this for migration from bots2.2.1 -\> 3.0.0, but works for
    all bots2.`*` installations.



### Windows procedure

1.	make a backup!
2.	rename existing installation
	-   existing bots-installation is in C:\\Python27\\Lib\\site-packages
	-   renamed bots directory to bots221
	-   also renamed existing directories for cherrypy, django, genshi.
3.	do a fresh install of bots3.0.0 installer (bots-3.0.0.win32.exe)
4.	copy old data to new installation.
	-   in C:\\Python27\\Lib\\site-packages new directories have been
	    installed (bots, django, cherrypy, genshi)
	-   copy directories botssys and usersys from bots221-directory to bots
	    directories. Everything can be overwritten.

5.	change settings
	-   use new config/bots.ini, adapt for your own values.
	-   use new config/settings.py, adapt for your own values. Especially
	    the database settings are important; the format is slightly
	    different (but similar enough to give no problem); critical is using
    	the 'ENGINE'-value of the new settings.py.

6. 	update the database.
	-   use command-prompt/dos-box
	-   goto directory C:\\Python27\\Scripts
	-   command-line: `C:\Python27\python bots-updatedb.py`
	-   should report that database is successful changed.
	    
If you use a 64-bits version of windows another option is to use
the 64-bits versions of python and bots.
    

### Linux procedure

1. make a backup!

2. rename existing installation
	-   existing bots-installation is in
    	/usr/local/lib/python2.7/dist-packages
	-   renamed bots directory to bots221
	-   for libraries: check you use at least django 1.3

3.	do a fresh install: see [installation
	procedure](StartInstallProcedure.md)

4. 	copy old data to new installation.
	-   in /usr/local/lib/python2.7/dist-packages new bots-directory is
    	installed.
	-   copy directories botssys and usersys from bots221-directory to bots
    	directories. Everything can be overwritten.
	-   mind your rights!

5. 	change settings
	-   use new config/bots.ini, adapt for your own values.
	-   use new config/settings.py, adapt for your own values. Especially
    	the database settings are important; the format is slightly
    	different (but similar enough to give no problem); critical is using
    	the 'ENGINE'-value of the new settings.py.

6. 	update the database.  
	command-line: `bots-updatedb.py`  
	should report that database is successful changed.

