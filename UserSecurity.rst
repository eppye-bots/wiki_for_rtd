User Rights
===========

To add Bots users, select **Users** on the **SysTasks** menu. The Change
User screen has a section called **Permissions** which contains the
following settings controlling that user's access.

Active
~~~~~~

If this box is checked, the user is able to log on to the webserver and
view run details. Note: A bug in version 3.1.0 prevents users with only
Active status from changing their own passwords. To be fixed in v3.2.0.

.. raw:: html

   <h3>

Staff status

.. raw:: html

   </h3>

These users may also see the Configuration and Run menu items, depending
on specific user permissions (see below). Only the permitted menu items
will be visible. If you do not give any extra permissions, only an empty
configuration menu is shown.

.. raw:: html

   <h3>

Superuser status

.. raw:: html

   </h3>

These users can also see the Systasks menu. They have access to all
Configuration and Run options without being specifically given
permission. The default user (bots) is a superuser. Recommendation:
Create user names according to your company policy. Disable the default
user or change the password; anybody can find out the default
user/password for bots!

.. raw:: html

   <h3>

User Permissions for Staff status users

.. raw:: html

   </h3>

Here you can add permissions for specific configuration objects. Only
some of the permissions shown in the list are relevant; they control
access to the corresponding configuration menu options. Any permissions
not listed below can be ignored as they have no effect in Bots GUI.
Permissions can be given directly to a user, or to a user group which is
then added to multiple users.

.. raw:: html

   <ul><li>

bots route

.. raw:: html

   </li><li>

bots channel

.. raw:: html

   </li><li>

bots translation

.. raw:: html

   </li><li>

bots partner

.. raw:: html

   </li><li>

bots confirm rule

.. raw:: html

   </li><li>

bots user code

.. raw:: html

   </li><li>

bots user code type

.. raw:: html

   </li><li>

bots mutex - gives access to the Run menu \* new in version 2.2.0

.. raw:: html

   </li></ul>

You can use the search box under Available user permissions, then select
the required permissions. Use the Ctrl-key to select multple items.
Normally, you would give add/change/delete permissions together for the
required configuration. eg. To allow a staff user to configure channels,
give these permissions.

.. raw:: html

   <pre><code>bots | channel | Can add channel<br>
   bots | channel | Can change channel<br>
   bots | channel | Can delete channel<br>
   </code></pre>

To allow a staff user access to the Run menu, give this special
permission. (mutex is a table that bots uses to indicate a database lock
while the engine runs)

.. raw:: html

   <pre><code>bots | mutex | Can change mutex<br>
   </code></pre>

 !!explain user groups!!
