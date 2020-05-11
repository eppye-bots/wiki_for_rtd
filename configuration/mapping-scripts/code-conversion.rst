Code Conversion
===============

Bots supports code conversions. The code conversion is done in a mapping script; maintenance for the codes can be done via ``bots-monitor->Configuration->User codes as list``.
Examples of code conversions are: convert internal currency codes to external currency code, convert internal customer number to external customer number.


**Code Maintenance in GUI**

First configure 2 code lists (``bots-monitor->Configuration->user codes by type``):

.. image:: ../../images/CCbytype.png

Make the code conversions (``bots-monitor->Configuration->user codes as list``):

.. image:: ../../images/CCaslist.png

**Example Code Conversion in Mapping Script**

.. code-block:: python

    import bots.transform as transform

    #convert currency code
    our_currency_code = inn.get({'BOTSID':'HEA','VALUTA':None})
    converted_currency_code = transform.ccode('Currency',our_currency_code)

    #convert internal article code to buyers article code:
    buyer_article_number = transform.ccode('LookupArticleNumber',our_article_number)

    #get description (in field 'attr1') for article
    description = transform.ccode('LookupArticleNumber',our_article_number,field='attr1')

    #code conversion also works via reverse lookup:
    our_article_number = transform.reverse_ccode('LookupArticleNumber',buyer_article_number)

    #return 'our_article_number' unconverted if not found in codelist:
    buyer_article_number = transform.ccode('LookupArticleNumber',our_article_number,safe=True)

    #if 'our_article_number' not found in codelist return value None:
    buyer_article_number = transform.ccode('LookupArticleNumber',our_article_number,safe=None)



**Code Conversion Functions**

**transform.ccode(codelist, value, field, safe)**

    Convert **value** to value in **field** using a user-maintained code list. Parameters:

    * *codelist*: codelist as in ``bots-monitor->Configuration->user`` codes by type.
    * *value*: code to be converted (should be in **leftcode**)
    * *field*: the field to return (if not specified: **rightcode**)
    * *safe*: determines what happens if code not found in code conversion. Options:
        * False (default): raise exception
        * True: return not-converted code
        * None: return None


**transform.reverse_ccode(codelist, value, field)**

    Same as transform.ccode(), but conversion is from **rightcode** to **field**.

**Changes in Code Conversion Functions**

These functions have changed over versions. The old functions are deprecated but still work.

.. csv-table::
    :header: "bots<2.1", "bots<3.0", "bots>=3.0"

    "codetconversion", "ccode", "ccode"
    "safecodetconversion", "safe_ccode", "ccode with parameter safe=True"
    "rcodetconversion", "reverse_ccode", "reverse_ccode"
    "safercodetconversion", "safe_reverse_ccode", "reverse_ccode with parameter safe=True"

