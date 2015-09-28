Recorddefs
----------

    Definition: *Recorddefs defines the layout of each record.*
    Recorddefs is required, except for grammars for editypes
    'templatehtml', 'xmlnocheck', 'jsonnocheck'. Recorddefs is a
    dictionary; key is record ID/tag, value is list of fields. There is
    always a field 'BOTSID' in a record; mostly BOTSID is the first
    field (fixed format is the exception).

    .. raw:: html

       </li></ul>

.. raw:: html

   <h3>

Some specifics for different editypes

.. raw:: html

   </h3>
   <ul><li>

edifact: record ID is edifact tag (DTM, BGM, etc).

.. raw:: html

   </li><li>

X12: record ID is the segment identifier

.. raw:: html

   </li><li>

Xml: record ID is xml-tag (without angle brackets).

.. raw:: html

   </li><li>

Fixed: bots has to know where record ID is. Default: first three
positions in record; this can be set with syntax parameters

.. raw:: html

   </li><li>

Csv: Csv/Excel does not always have a record ID (all records in an
edi-file are of the same type). Bots uses the name of the record as
BOTSID if you use syntax parameter:

.. raw:: html

   <pre><code>'noBOTSID':True<br>
   </code></pre></li></ul>

.. raw:: html

   <h3>

For each field

.. raw:: html

   </h3>

Each field is a list of:

.. raw:: html

   <ol><li>

field ID; has to be unique (bots checks for this).

.. raw:: html

   </li><li>

M/C: mandatory or conditional.

.. raw:: html

   </li><li>

length. Examples:

.. raw:: html

   <pre><code>['field name','C', 9, 'A'],       #max length<br>
   ['field name','C', (3,9), 'A'],   #min length, max length. Use eg as:<br>
   ['field name','C', (9,9), 'A'],   #field length should always be 9<br>
   ['field name','C', 8.3, 'N'],     #length max 8 field, must have 3 decimals. <br>
   </code></pre>
   </li><li>

format. Different per editype. Especially edifact, x12 and tradacoms
have their own formatting codes, just use these. For csv, fixed, xml etc
no standard formats exists, so bots uses these formats:

.. raw:: html

   <ul><li>

A (or AN): alphanumeric.

.. raw:: html

   </li><li>

AR: right aligned alphanumeric (fixed only)

.. raw:: html

   </li><li>

N: fixed decimals

.. raw:: html

   <ul><li>

Numeric

.. raw:: html

   </li><li>

Fixed numbers of decimals. If no decimals are indicated: integer

.. raw:: html

   </li><li>

Incoming: format is checked.

.. raw:: html

   </li><li>

Outgoing: bots formats this (rounding if needed, add leading zeros)

.. raw:: html

   </li></ul></li><li>

NL: (for fixed only) as fixed decimals, left aligned, trailing blancs

.. raw:: html

   </li><li>

NR: (for fixed only) as fixed decimals, right aligned, leading blancs

.. raw:: html

   </li><li>

R: floating point

.. raw:: html

   <ul><li>

Numeric

.. raw:: html

   </li><li>

May have any number of decimals

.. raw:: html

   </li><li>

Bots does no checking of formatting.

.. raw:: html

   </li></ul></li><li>

RL: (for fixed only) as floating point, left aligned, trailing blancs

.. raw:: html

   </li><li>

RR: (for fixed only) as floating point, left aligned, leading blancs

.. raw:: html

   </li><li>

I: fixed decimals implicit. Example:

.. raw:: html

   <pre><code>['field name','C', 8.2, 'I'],   #max 8 long, last 2 positions are decimals; eg for an amount.<br>
                                   #Valid is eg:  12345<br>
                                   #Bots converts this to 123.45 (and vice versa)<br>
   </code></pre>
   <ul><li>

Numeric

.. raw:: html

   </li><li>

Fixed number of decimals. Is converted from/to 'normal' amount; rounded
if outgoing.

.. raw:: html

   </li><li>

There is no decimal sign in the field, the number of decimals is
implicit from the definition. Eg:

.. raw:: html

   </li><li>

Can be negative

.. raw:: html

   </li></ul></li><li>

D (or DT): date. Either 6 or 8 positions; format YYMMDD or CCYYMMDD.
Bots checks for valid dates both in- en outgoing.

.. raw:: html

   </li><li>

T (or TM): time. Either 4 or 6 positions; format HHMM or HHMMSS. Bots
checks for valid times both in- en outgoing.

.. raw:: html

   </li></ul></li></ol>

.. raw:: html

   <h3>

Composite fields

.. raw:: html

   </h3>

Edifact, x12 and tradacoms have composite fields. Example:

.. raw:: html

   <pre><code>['S005', 'C',                      #composite field<br>
       [<br>
       ['S005.0022', 'M', 14, 'AN'],  #subfield nr1<br>
       ['S005.0025', 'C', 2, 'AN'],   #subfield nr2<br>
       ]],<br>
   <br>
   </code></pre>

A composite has:

.. raw:: html

   <ol><li>

field ID; has to be unique (bots checks for this).

.. raw:: html

   </li><li>

M/C (mandatory/conditional).

.. raw:: html

   </li><li>

a list of subfields. Note: Bots requires that each composite ID and
sub-field has an unique ID. If a composite occurs more than once, do eg
like:

.. raw:: html

   <pre><code>['C090', 'C', [                        #composite contains 2 subfields with same ID<br>
       ['C090.3286#1', 'M', 70, 'AN'],<br>
       ['C090.3286#2', 'C', 70, 'AN'],<br>
       ]],<br>
   ['C542#1', 'M', [                      #composite occurs twice <br>
       ['C542.9425#1', 'M', 3, 'AN'],<br>
       ['C542.9424#1', 'C', 35, 'AN'],<br>
       ]],<br>
   ['C542#2', 'C', [                      #composite occurs twice<br>
       ['C542.9425#2', 'M', 3, 'AN'],<br>
       ['C542.9424#2', 'C', 35, 'AN'],<br>
       ]],<br>
   </code></pre></li></ol>

.. raw:: html

   <h3>

Details of field format handling

.. raw:: html

   </h3>
   <ul><li>

M/C of fields are always checked.

.. raw:: html

   </li><li>

min/max length of field are always checked.

.. raw:: html

   </li><li>

numerical:

.. raw:: html

   <ul><li>

'-' is accepted both at beginning and end. Bots outputs only leading '-'

.. raw:: html

   </li><li>

'+' is accepted at beginning. Bots does not output '+'

.. raw:: html

   </li><li>

thousands separators are removed if specified in syntax-parameter
'triad' (see above).

.. raw:: html

   </li><li>

Bots does not output thousands separators

.. raw:: html

   </li><li>

default decimal separator is '.'; use syntax-parameter 'decimaal' to
change this ('decimaal' is Dutch, sorry about that. Noticed to late to
change ;-)). Internally bots only uses/accepts decimal point!

.. raw:: html

   </li><li>

(incoming) leading zeros are removed

.. raw:: html

   </li><li>

(incoming) trailing zeros are kept

.. raw:: html

   </li><li>

'.45' is converted to '0.45'.

.. raw:: html

   </li><li>

'4.' is converted to '4'.

.. raw:: html

   </li><li>

Note that eg edifact numeric lengths do NOT include decimal sign and
negative...

.. raw:: html

   </li></ul></li></ul>

.. raw:: html

   <h3>

Utility for positions in fixed records

.. raw:: html

   </h3>

A grammar does not contains the position/offset of each field in a fixed
record, but it sure is useful to have this. Add this code to the bottom
of the grammar and run/execute the code:

.. raw:: html

   <pre><code>if __name__ == "__main__":<br>
       for key, record in recorddefs.items():<br>
           length = 0<br>
           for field in record:<br>
               print '           ', field, '      #pos',length+1, length + field[2]<br>
               length += field[2]<br>
           print 'Record',key,'  has length ',length, '\n'<br>
   </code></pre>

Slightly different version - output can be pasted back into grammar

.. raw:: html

   <pre><code>if __name__ == "__main__":<br>
       space = 0<br>
       for key, record in recorddefs.items():<br>
           for field in record:<br>
               space = max(space,len(str(field))+1)<br>
       for key, record in recorddefs.items():<br>
           length = 0<br>
           print '    \'' + key + '\':['<br>
           for field in record:<br>
               print '           ', (str(field) + ',').ljust(space), ' # pos',length+1, '-', length + field[2]<br>
               length += field[2]<br>
           print '    ],'<br>
   </code></pre>

