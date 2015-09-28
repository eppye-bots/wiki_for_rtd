Chained Translations
--------------------

    Definition: *chained translations translate one incoming format to
    multiple outgoing formats.*

Eg: translate edi-order to in-house format AND send an email to inform
sales representative. To use this bots uses the 'alt'. How this works:

.. raw:: html

   <ul><li>

receive incoming file

.. raw:: html

   </li><li>

do a translation (using mapping script)

.. raw:: html

   </li><li>

mapping script returns alt-value

.. raw:: html

   </li><li>

do another translation using the alt-value. Background information:
TranslationRules how bots determines what to translate.

.. raw:: html

   </li></ul>

   <h3>

By example

.. raw:: html

   </h3>

   <ul><li>

Set up first translation rule (to csv-format) as usual:

.. raw:: html

   <ul><li>

translate x12-850 to csv-orders using mapping script 850\_2\_csv

.. raw:: html

   </li></ul></li><li>

at end of mapping script 850\_2\_csv:

.. raw:: html

   <pre><code>  return 'do_email_translation'        #alt-value is returned<br>
   </code></pre>
   </li><li>

Set up the second translation rule:

.. raw:: html

   <ul><li>

translate x12-850 to csv-orders using mapping script 850\_2\_email where
alt=do\_email\_translation

.. raw:: html

   </li></ul></li></ul>

By returning the alt-value 'do\_email\_translation' mapping script
850\_2\_csv triggers the 2nd translation (with mapping script
850\_2\_email).

.. raw:: html

   <h3>

Plugin

.. raw:: html

   </h3>

In plugin edifact\_ordersdesadvinvoic on bots sourceforge site:

.. raw:: html

   <ol><li>

incoming is edifact orders.

.. raw:: html

   </li><li>

translate fixed inhouse format.

.. raw:: html

   </li><li>

translate to edifact APERAK/acknowledgement (if acknowledgement is
asked).

.. raw:: html

   </li></ol>

   <h3>

Details

.. raw:: html

   </h3>
   <ul><li>

Of course it is possible to 'chain' more than one translation.

.. raw:: html

   </li><li>

I have used this to do complex 'sorts' on incoming documents, eg:

.. raw:: html

   <ul><li>

write/sort to multiple outgoing messages sorting for destination of
goods

.. raw:: html

   </li></ul></li><li>

Note: in this type of set-up multiple formats are outgoing, you'll want
to use a composite route.

.. raw:: html

   </li></ul>

.. raw:: html

   <h2>

Special Chained Translations

.. raw:: html

   </h2>

You can also return an alt value that is a python dict. The dict must
contain 'type' and 'alt' strings; there are several special types
available for different processing requirements.

.. raw:: html

   <h3>

out\_as\_inn

.. raw:: html

   </h3>

Do chained translation: use the out-object as inn-object, new
out-object. Use cases:

.. raw:: html

   <ol><li>

Detected error in incoming file; use out-object to generate warning
email.

.. raw:: html

   </li><li>

Map inputs to standard format, also map standard format to human
readable version (eg. html template) Both out-objects are output by Bots
and can be sent to same or different channels using channel filtering.

.. raw:: html

   <pre><code>    # if the first output is not needed to send somewhere, discard it<br>
       # omit this step and you will get both outputs<br>
       from bots.botsconfig import *<br>
       out.ta_info['statust'] = DONE<br>
   <br>
       # use output of first mapping as input of second mapping<br>
       return {'type':'out_as_inn','alt':'do_email_translation'}<br>
   </code></pre></li></ol>

   <h3>

no\_check\_on\_infinite\_loop

.. raw:: html

   </h3>

Do chained translation: allow many loops with same alt-value. Normally,
Bots will detect and prevent this, by stopping after 10 iterations of
the loop. You are disabling this safety feature, so your mapping script
will have to handle this correctly to ensure the looping is not
infinite.

.. raw:: html

   <pre><code>    # we MUST have a way to exit the loop!<br>
       if (some condition):<br>
           return<br>
   <br>
       # loop through this mapping multiple times...<br>
       return {'type':'no_check_on_infinite_loop','alt':'repeat'}<br>
   </code></pre>

