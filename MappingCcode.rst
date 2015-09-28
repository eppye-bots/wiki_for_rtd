Code conversion
---------------

Bots supports code conversions. The code conversion is done in a mapping
script; maintenance for the codes can be done via
*bots-monitor->Configuration->User codes as list*.

This page contains 3 examples of code conversions:

.. raw:: html

   <ol><li>

convert currency code list.

.. raw:: html

   </li><li>

convert internal article code to buyers article code.

.. raw:: html

   </li><li>

convert internal article code to description.

.. raw:: html

   </li></ol>

.. raw:: html

   <h3>

Code maintenance in GUI

.. raw:: html

   </h3>

First configure 2 code lists (bots-monitor->Configuration->user codes by
type):

 Make the code conversions (bots-monitor->Configuration->user codes as
list):

.. raw:: html

   <h3>

Code conversion in mapping script

.. raw:: html

   </h3>
   <pre><code>    import bots.transform as transform<br>
   <br>
       #convert currency code<br>
       our_currency_code = inn.get({'BOTSID':'HEA','VALUTA':None})<br>
       converted_currency_code = transform.ccode('Currency',our_currency_code)<br>
   <br>
       #convert internal article code to buyers article code:<br>
       buyer_article_number = transform.ccode('LookupArticleNumber',our_article_number)<br>
   <br>
       #get description (in field 'attr1') for article<br>
       description = transform.ccode('LookupArticleNumber',our_article_number,field='attr1')<br>
   <br>
       #code conversion also works via reverse lookup:<br>
       our_article_number = transform.reverse_ccode('LookupArticleNumber',buyer_article_number)<br>
   </code></pre>

.. raw:: html

   <h3>

Codeconversion functions

.. raw:: html

   </h3>

   <h4>

transform.ccode(codelist, value, field, safe)

.. raw:: html

   </h4>

Convert 'value' to value in 'field' using a user-maintained code list.
Parameters:

.. raw:: html

   <ul><li>

codelist: codelist as in bots-monitor->Configuration->user codes by
type.

.. raw:: html

   </li><li>

value to be converted (should be in 'leftcode')

.. raw:: html

   </li><li>

field: the field to lookup (if not specified: 'rightcode')

.. raw:: html

   </li><li>

safe: if False (default): raise exception when value is in found in
codelist. If True: just return 'value'. Example of usage for leftcode to
rightcode:

.. raw:: html

   <pre><code>    transform.ccode('articles','8712345678906') <br>
   </code></pre>

Example of usage for leftcode to attr1:

.. raw:: html

   <pre><code>    transform.ccode('articles','8712345678906','attr1') <br>
   </code></pre></li></ul>

   <h4>

transform.reverse\_ccode(codelist, value, field)

.. raw:: html

   </h4>

as transform.ccode(), but conversion is from 'rightcode' to 'field'.

.. raw:: html

   <h3>

Changes in codeconversion functions

.. raw:: html

   </h3>

Note: These functions have changed over versions. The old functions are
deprecated but still work.

.. raw:: html

   <table><thead><th> 

bots<2.1

.. raw:: html

   </th><th> 

bots<3.0

.. raw:: html

   </th><th> 

bots>=3.0

.. raw:: html

   </th></thead><tbody>
   <tr><td>

codetconversion

.. raw:: html

   </td><td>

ccode

.. raw:: html

   </td><td>

ccode

.. raw:: html

   </td></tr>
   <tr><td>

safecodetconversion

.. raw:: html

   </td><td>

safe\_ccode

.. raw:: html

   </td><td>

ccode with parameter safe=True

.. raw:: html

   </td></tr>
   <tr><td>

rcodetconversion

.. raw:: html

   </td><td>

reverse\_ccode

.. raw:: html

   </td><td>

reverse\_ccode

.. raw:: html

   </td></tr>
   <tr><td>

safercodetconversion

.. raw:: html

   </td><td>

safe\_reverse\_ccode

.. raw:: html

   </td><td>

reverse\_ccode with parameter safe=True

.. raw:: html

   </td></tr>

