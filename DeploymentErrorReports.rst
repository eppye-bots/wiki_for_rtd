Receive email notifications for errors in edi
---------------------------------------------

When bots runs scheduled, it is cumbersome to keep checking for errors
in the bots-monitor. It is possible to receive an email-report in case
of errors. Configure this:

.. raw:: html

   <ol><li>

Set option 'sendreportiferror' in bots/config/bots.ini to True.

.. raw:: html

   </li><li>

In bots/config/settings.py set relevant data for email, eg like:

.. raw:: html

   <pre><code>MANAGERS = (    #bots will send error reports to the MANAGERS<br>
       ('name_manager', 'myemailaddress@gmail'),<br>
       )<br>
   EMAIL_HOST = 'smtp.gmail.com'             #Default: 'localhost'<br>
   EMAIL_PORT = '587'             #Default: 25<br>
   EMAIL_USE_TLS = True       #Default: False<br>
   EMAIL_HOST_USER = 'username'        #Default: ''. Username to use for the SMTP server defined in EMAIL_HOST. If empty, Django won't attempt authentication.<br>
   EMAIL_HOST_PASSWORD = '*******'    #Default: ''. PASSWORD to use for the SMTP server defined in EMAIL_HOST. If empty, Django won't attempt authentication.<br>
   SERVER_EMAIL = 'botserrors@gmail.com'           #Sender of bots error reports. Default: 'root@localhost'<br>
   EMAIL_SUBJECT_PREFIX = ''   #This is prepended on email subject.<br>
   </code></pre>
   </li><li>

To test if it works OK, restart the bots-webserver and
bots-monitor->Systasks->Send test report. (I know, the restarting is
annoying.).

.. raw:: html

   </li></ol>

Note: Email notifications are not sent while running acceptance tests.
