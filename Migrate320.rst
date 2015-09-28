Bots 3.2.0rc was released 2014-03-22. Bots 3.2.0rc2 was released
2014-05-27. Bots 3.2.0 was released 2014-09-02.

Migration notes:

.. raw:: html

   <ol><li>

bots 3.2.0 is suited for django 1.4, 1.5, 1.6 and 1.7. Support for
Django 1.3 is dropped.

.. raw:: html

   </li><li>

in existing settings.py django requires parameter 'ALLOWED\_HOSTS'. Add
this as eg:

.. raw:: html

   <pre><code>    ALLOWED_HOSTS = ['*']<br>
   </code></pre>
   </li><li>

For SQLite no database migration is needed. For MySQL and PostgreSQL: in
table unique, field 'domein' should be changed to 70 positions (was: 35)
if using option to have in-communication connect failures reported after
xx times (field 'Max failures' in channels).

.. raw:: html

   </li><li>

Python 2.5 is not supported anymore. use 2.6, preferably 2.7.

.. raw:: html

   </li><li>

Bots does not support python > 3 (yet). Reason is that python MySQL
connector is not suited for python 3 (yet).
