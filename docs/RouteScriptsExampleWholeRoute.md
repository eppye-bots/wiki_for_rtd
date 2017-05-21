## Example route script that takes over whole route ##

```
# imports needed for some functions below
from bots.botsconfig import *
import bots.transform as transform
import bots.botsglobal as botsglobal
import bots.botslib as botslib
import bots.cleanup as cleanup
import bots.pluglib as pluglib
import os
import time

def main(routedict,*args,**kwargs):
    # if main is present, it takes over the whole route (nothing is done in route except this function).
    # for example, create a daily route that does a backup and cleanup

    # Prevent this script from accidentally running more than once per day
    if transform.persist_lookup(routedict['idroute'],'run_date') != time.strftime('%Y%m%d'):
        transform.persist_add_update(routedict['idroute'],'run_date',time.strftime('%Y%m%d'))

        # backup directory and subdirectory - one per weekday gives a 7 day rolling backup
        backup_dir = botslib.join(botsglobal.ini.get('directories','botssys'), 'backup')
        makedir(backup_dir) 
        backup_dir = botslib.join(backup_dir, time.strftime('%w-%a'))
        makedir(backup_dir)

        # Create a bots backup (as a plugin)
        botsglobal.logger.info('Create a bots backup')
        pluglib.plugoutcore({
             'databaseconfiguration': True,
             'umlists': True,
             'fileconfiguration': True,
             'infiles': False,
             'charset': False,
             'databasetransactions': False,
             'data': False,
             'logfiles': True,
             'config': True,
             'database': True,
             'filename': botslib.join(backup_dir,'bots-backup.zip')})

        # Do cleanup, if scheduled daily
        # In bots.ini set whencleanup=daily (other values are always or never)
        if botsglobal.ini.get('settings','whencleanup','always') == 'daily':
            botsglobal.logger.info(u'Cleanup of database and files')
            cleanup.cleanup()

def makedir(dir):
    try: os.makedirs(dir) 
    except: pass
```