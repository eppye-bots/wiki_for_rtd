## Upgrade bots version 2.`*`.`*` -> 2.2.0

### Procedure

**NOTE: please make backup first!**

for all updates: settings.py **HAS** to be changed. One line has to be added (at end of file):

```
  TEMPLATE_CONTEXT_PROCESSORS = (
    "django.core.context_processors.auth",
    "django.core.context_processors.debug",
    "django.core.context_processors.i18n",
    "django.core.context_processors.media",
    "django.core.context_processors.request",
    "bots.bots_context.set_context",    #THIS LINE IS ADDED!
    )
```

1.  Update plugin:
    -   Get the plugin at [sourceforge](http://sourceforge.net/projects/bots/files/bots%20open%20source%20edi%20software/2.2.0).
    -   Mind there are 2 version of the plugin, depending upon the version of django you use.
    -   Read like a normal plugin (bots-monitor->systasks->read plugin).
    -   Bots-monitor will give an error...nasty but upgrade is done.
    -   Stop the web-server.
    -   Edit bots/config/settings.py (See above)
    -   Restart bots-webserver.
1.  For windows:
    -   Get the installer at [sourceforge](http://sourceforge.net/projects/bots/files/bots%20open%20source%20edi%20software/2.2.0).
    -   Install new version.
    -   Django is upgraded to 1.3.1
    -   Database and mappings are not changed
    -   Configuration files have not been changed
    -   Edit bots/config/settings.py (See above)

### Compatibility

Version 2.2.0 is upward compatible with previous versions in 2.`*`.`*`-series:

-   no data migration needed
-   grammars, translations etc mostly will work as before

### Compatibility problems

1.  when upgrading from 2.0.`*` see [migration to 2.1.0](Migrate210.md)
1.  as mentioned above: new line has to be added in settings.py in TEMPLATE\_CONTEXT\_PROCESSORS

### Deprecated 
1.  django 1.1.`*`; use django > 1.2.0, see for [instructions](MigrateDjango.md)
1.  editype: database (=database connector with SQLalchemy). Use editype db; if wished you can use SQLalchemy in this new database connector.
1.  code conversion via file (in bots/usersys/codeconversions). Use codeconversion via ccode table: better, faster, more flexible.
1.  editype template (with library 'kid'); use editype template-html (with library Genshi) instead. 
    Genshi is quite simular to kid, see for [instructions](MigrateKidGenshi.md)
1.  communication via intercommit (type intercommit). If needed, a plugin can be provided.

### Changes in bots.ini

You can use your old bots.ini with no problem, reasonable defaults have been used. New options added in 2.2.0:

```
[webserver]

#settings for logging of bots-webserver
#console logging on (True) or off (False); default is True.
webserver_log_console = True
#webserver_log_console_level: level for logging to console/screen. Values: DEBUG,INFO,STARTINFO,WARNING,ERROR or CRITICAL. Default: STARTINFO 
#actually useful: WARNING: only start-up text; info gives more info
webserver_log_console_level = STARTINFO

# to customise name of botslogo html file (default: bots/botslogo.html)
botslogo = bots/botslogo.html
# text displayed on right of bots logo. Useful to indicate different environments: TEST, PRODUCTION. Default: no text
environment_text = 

#when True, the run menu contains entries to run each route indivudually. Default: False
menu_all_routes = False

[custommenus]
#it is possible to add a custom menu to the default bots menu. Features
#1. the menuname to appear on the menu bar in bots monitor; Default: Custom. Eg:
#menuname = MyMenu
#2. Entries ins the custom menu: all "name: value" entries in this section will be added to the custom menu in bots monitor. Eg:
#Incoming = /incoming/?all
#3. Menu divider lines can be added with special value "---". Eg:
#divider1 = ---
# note: sequence of entries is preserved, but case of menu entry is not; title case will be applied
```
