## Code conversion

Bots supports code conversions. The code conversion is done in a mapping script;
maintenance for the codes can be done via _bots-monitor-\>Configuration-\>User codes as list_.

This page contains 3 examples of code conversions:

1.  convert currency code list.
2.  convert internal article code to buyers article code.
3.  convert internal article code to description.


### Code maintenance in GUI

First configure 2 code lists (*bots-monitor-\>Configuration-\>user codes
by type*):
 ![](CCbytype.png)
 Make the code conversions (*bots-monitor-\>Configuration-\>user codes
as list*):
 ![](CCaslist.png)

### Code conversion in mapping script

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



### Codeconversion functions

#### transform.ccode(codelist, value, field, safe)

Convert 'value' to value in 'field' using a user-maintained code list.  
Parameters:

-   codelist: codelist as in *bots-monitor-\>Configuration-\>user codes
    by type*.
-   value to be converted (should be in 'leftcode')
-   field: the field to lookup (if not specified: 'rightcode')
-   safe: if False (default): raise exception when value is in found in
    codelist. If True: just return 'value'.
    
    Example of usage for leftcode to rightcode:

            transform.ccode('articles','8712345678906') 

    Example of usage for leftcode to attr1:

            transform.ccode('articles','8712345678906','attr1') 

#### transform.reverse\_ccode(codelist, value, field)

as transform.ccode(), but conversion is from 'rightcode' to 'field'.


### Changes in codeconversion functions

Note: These functions have changed over versions. The old functions are
deprecated but still work.

bots < 2.1          |bots < 3.0          |bots >= 3.0
--------------------|--------------------|-----------
codetconversion     |ccode               |ccode
safecodetconversion |safe\_ccode         |ccode with parameter safe=True
rcodetconversion    |reverse\_ccode      |reverse\_ccode
safercodetconversion|safe\_reverse\_ccode|reverse\_ccode with parameter safe=True

