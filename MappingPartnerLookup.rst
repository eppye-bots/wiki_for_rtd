Partner look-up (bots>=3.0)
---------------------------

Often there is a need to retrieve data from a partner, using a
IDpartner. Think of: \* check if partner is active \* get name/address
of partner \* get senderID for partner

Recipe
~~~~~~

Get the value in field 'attr1' for the IDpartner. See partners in
bots-monitor->Configuration->Partners for possible fields.

.. raw:: html

   <pre><code>transform.partnerlookup('buyer1','attr1',safe=True) <br>
   </code></pre>

Check if a partner exists, and is active. If not, raise an exception.

.. raw:: html

   <pre><code>transform.partnerlookup('buyer1','active') <br>
   </code></pre>


   <table><thead><th> 

Value for safe

.. raw:: html

   </th><th> 

If a record matching your lookup does not exist, or the requested field
is empty

.. raw:: html

   </th></thead><tbody>
   <tr><td>

safe=False(default)

.. raw:: html

   </td><td>

An exception is raisedYou can check for this in your script if required
and take action

.. raw:: html

   </td></tr>
   <tr><td>

safe=True

.. raw:: html

   </td><td>

No exception is raised, just returns the lookup valueeg. to lookup a
user defined field for partner translation on some partners

.. raw:: html

   </td></tr>
   <tr><td>

safe=None(Bots>=3.2)

.. raw:: html

   </td><td>

No exception is raised, returns Noneeg. to get address lines where not
all partners have addresses, but this is not an error

.. raw:: html

   </td></tr></tbody></table>

   <h3>

Lookup using a field other than IDpartner

.. raw:: html

   </h3>

This is similar to reverse code conversion, but can look up any partner
field and return any other partner field. Beware of performance issues
if you have a large number of partners. Also there may be multiple
matches if the lookup is not unique, only one is returned. Get the value
in field 'name' by looking up value in 'attr2'.

.. raw:: html

   <pre><code>transform.partnerlookup('my attribute','name','attr2',safe=True) <br>
   </code></pre>

   <h3>

Notes

.. raw:: html

   </h3>
   <ul><li>

In bots<3.0 this was possible using code conversion. But this could lead
to situations where partners where both in
bots-monitor->Configuration->Partners & groups and in code conversions.

.. raw:: html

   </li><li>

partners have more fields in bots>=3.0 like name, address, 'free'
fields.
