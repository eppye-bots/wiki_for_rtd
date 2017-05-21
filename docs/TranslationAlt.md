## Chained Translations

> Definition: _chained translations
translate one incoming format to multiple outgoing formats._ 

Eg: translate edi-order to in-house format AND send an email to inform sales
representative.  

To use this bots uses the 'alt'.  
How this works:

-   receive incoming file
-   do a translation (using mapping script)
-   mapping script returns alt-value
-   do another translation using the alt-value.
    
Background information: [how bots determines what
to translate](TranslationRules.md).

### By example

-   Set up first translation rule (to csv-format) as usual:
    -   translate x12-850 to csv-orders using mapping script
        850\_2\_csv
-   at end of mapping script 850\_2\_csv:

          return 'do_email_translation'        #alt-value is returned

-   Set up the second translation rule:
    -   translate x12-850 to csv-orders using mapping script
        850\_2\_email **where alt=do\_email\_translation**

By returning the alt-value 'do\_email\_translation' mapping script
850\_2\_csv triggers the 2nd translation (with mapping script
850\_2\_email).

### Plugin

In plugin *edifact\_ordersdesadvinvoic* on [bots sourceforge
site](http://sourceforge.net/projects/bots/files/plugins/):

1. 	incoming is edifact orders.
2.  translate fixed inhouse format.
3.  translate to edifact APERAK/acknowledgement (if acknowledgement is
    asked).

### Details

-   Of course it is possible to 'chain' more than one translation.
-   I have used this to do complex 'sorts' on incoming documents, eg:
    -   write/sort to multiple outgoing messages sorting for destination
        of goods
-   Note: in this type of set-up multiple formats are outgoing, you'll
    want to use a [composite route](RoutesComposite.md).


### Special Chained Translations

You can also return an alt value that is a python dict. The dict must
contain 'type' and 'alt' strings; there are several special types
available for different processing requirements.


### out\_as\_inn

Do chained translation: use the out-object as inn-object, new
out-object.  
Use cases:

1.  Detected error in incoming file; use out-object to generate warning
    email.
2.  Map inputs to standard format, also map standard format to human
    readable version (eg. html template)
    Both out-objects are output by Bots and can be sent to same or
    different channels using channel filtering.

            # if the first output is not needed to send somewhere, discard it
            # omit this step and you will get both outputs
            from bots.botsconfig import *
            out.ta_info['statust'] = DONE

            # use output of first mapping as input of second mapping
            return {'type':'out_as_inn','alt':'do_email_translation'}


### no\_check\_on\_infinite\_loop

Do chained translation: allow many loops with same alt-value.  
Normally, Bots will detect and prevent this, by stopping after 10
iterations of the loop. You are disabling this safety feature, so your
mapping script will have to handle this correctly to ensure the looping
is not infinite.  

        # we MUST have a way to exit the loop!
        if (some condition):
            return

        # loop through this mapping multiple times...
        return {'type':'no_check_on_infinite_loop','alt':'repeat'}
