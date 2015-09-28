Migrate Django to version 1.3 or greater
========================================

-  `Remove <https://docs.djangoproject.com/en/1.3/topics/install/#remove-any-old-versions-of-django>`__
   the 1.1 version of Django
-  `Download <https://www.djangoproject.com/download/>`__ new version.

   -  Mind: bots 2.2.0 does not support Django 1.4.\ ``*``.
   -  Django version 1.3.1 is tested and recommended.

-  `Install <https://docs.djangoproject.com/en/1.3/topics/install/#install-the-django-code>`__
   the new version
-  `Restart <StartGetBotsRunning#Start_bots-monitor_(including_bots-webserver).md>`__
   the bots webserver

Be sure to use the correct bots upgrade plugin to match the version of
Django you have installed.

Bots includes copies of some Django files in it's directory structure.
You may need to refresh these from your current Django version if you
notice any admin interface "bugs". (eg. selection checkboxes not working
correctly).

-  Copy from: -packages
-  Copy to: -packages
-  Include sub-directories: css, img, js

