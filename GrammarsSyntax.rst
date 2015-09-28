Syntax parameters
-----------------

Syntax contains parameters that are used in reading or writing
edi-files. The complete list of syntax parameters including default
values is in bots/grammars.py (in the classes of the editypes). Syntax
is a python dict (dictionary). Example of syntax parameters:

.. raw:: html

   <pre><code>syntax = { <br>
           'charset'                  : 'uft-8', #character set is utf-8<br>
           'checkfixedrecordtooshort' : True,    #check if fixed record is to short<br>
           'indented'                 : True,    #xml: produced indented output<br>
           'decimaal'                 : ',',     #decimal sign is ', '<br>
           }<br>
   </code></pre>

.. raw:: html

   <h2>

Syntax parameters usage and overriding

.. raw:: html

   </h2>

Syntax parameters can be set at different places; these settings
override (somewhat luke CSS). The order in which overriding is done:

.. raw:: html

   <ul><li>

default values are in bots/grammars.py (per editype). Do not change
these values!

.. raw:: html

   </li><li>

envelope grammar (eg for x12: bots/usersys/grammars/x12/x12.py, for
edifact: bots/usersys/grammars/edifact/edifact.py)

.. raw:: html

   </li><li>

message grammar

.. raw:: html

   </li><li>

frompartner grammar (eg in bots/usersys/partners/x12/partnerID.py)

.. raw:: html

   </li><li>

topartner grammar (eg in bots/usersys/partners/x12/partnerID.py)

.. raw:: html

   </li></ul>

   <h4>

Example 1: edifact charset

.. raw:: html

   </h4>
   <ul><li>

default value is UNOA

.. raw:: html

   </li><li>

value in envelope (edifact.py) is UNOA

.. raw:: html

   </li><li>

for invoices: a description is used so the message grammar for invoices
has charset UNOC

.. raw:: html

   </li><li>

retailer ABC insists on receiving invoices as UNOA, so this is indicated
in the topartner grammar.

.. raw:: html

   </li></ul>

   <h4>

Example 2: x12 element separator

.. raw:: html

   </h4>
   <ul><li>

in grammar.py: 'field\_sep':'\*' (bots default value)

.. raw:: html

   </li><li>

in x12.py: 'field\_sep':'\|' (default value company uses when sending
x12)

.. raw:: html

   </li><li>

retailer ABC insists: 'field\_sep':'07' (that is , or BEL)

.. raw:: html

   </li></ul>

.. raw:: html

   <h2>

List of most useful syntax parameters

.. raw:: html

   </h2>
   <table><thead><th> 

Parameter

.. raw:: html

   </th><th> 

In or out

.. raw:: html

   </th><th> 

Description

.. raw:: html

   </th></thead><tbody>
   <tr><td>

add\_crlfafterrecord\_sep

.. raw:: html

   </td><td>

Out

.. raw:: html

   </td><td>

put extra character after a record/segment separator. Value: string,
typically '' or ''. I use this for x12/edifact while testing: output is
better to read. Most partenrs can handles these file, but they are
slightly bigger. See also parameter 'indent'.

.. raw:: html

   </td></tr>
   <tr><td>

acceptspaceinnumfield

.. raw:: html

   </td><td>

In

.. raw:: html

   </td><td>

Do not raise error when numeric field contains only spaces but assume
value is 0

.. raw:: html

   </td></tr>
   <tr><td>

allow\_lastrecordnotclosedproperly

.. raw:: html

   </td><td>

In

.. raw:: html

   </td><td>

(csv) allows last record not to have record separator

.. raw:: html

   </td></tr>
   <tr><td>

charset

.. raw:: html

   </td><td>

In

.. raw:: html

   </td><td>

charset to use; (edifact, xml) is overridden by charset-declaration in
content.

.. raw:: html

   </td></tr>
   <tr><td>                  </td><td>

Out

.. raw:: html

   </td><td>

charset to use in output. Bots is quite strict in this.

.. raw:: html

   </td></tr>
   <tr><td>

checkcharsetin

.. raw:: html

   </td><td>

In

.. raw:: html

   </td><td>

what to do for chars not in charset. Possible values 'strict' (gives
error) or 'ignore' (skip the characters not in the charset) or
'botsreplace' (replace with char as set in bots.ini; default is space)

.. raw:: html

   </td></tr>
   <tr><td>

checkcharsetout

.. raw:: html

   </td><td>

Out

.. raw:: html

   </td><td>

what to do for chars not in charset. Possible values 'strict' (gives
error), 'ignore' (skip the characters not in the charset) or
'botsreplace' (replace with char as set in bots.ini; default is space)

.. raw:: html

   </td></tr>
   <tr><td>

checkfixedrecordtoolong

.. raw:: html

   </td><td>

In

.. raw:: html

   </td><td>

(fixed): warn if record too long. Possible values: True/False, default:
True

.. raw:: html

   </td></tr>
   <tr><td>

checkfixedrecordtooshort

.. raw:: html

   </td><td>

In

.. raw:: html

   </td><td>

(fixed): warn if record too short. Possible values: True/False, default:
False

.. raw:: html

   </td></tr>
   <tr><td>

checkunknownentities

.. raw:: html

   </td><td>

In/out

.. raw:: html

   </td><td>

(xml,JSON) skip unknown attributes/elements (instead of raising an
error)

.. raw:: html

   </td></tr>
   <tr><td>

contenttype

.. raw:: html

   </td><td>

Out

.. raw:: html

   </td><td>

content-type of translated file; used as mime-envelope of email

.. raw:: html

   </td></tr>
   <tr><td>

decimaal

.. raw:: html

   </td><td>

In/Out

.. raw:: html

   </td><td>

decimal point; default is '.'. For edifact: read from UNA-string if
present.

.. raw:: html

   </td></tr>
   <tr><td>

endrecordID

.. raw:: html

   </td><td>

In

.. raw:: html

   </td><td>

(fixed) end position of record ID; value: number, default 3. See
startrecordID

.. raw:: html

   </td></tr>
   <tr><td>

envelope

.. raw:: html

   </td><td>

Out

.. raw:: html

   </td><td>

envelope to use; if nothing specified: no envelope - files are just
copied/appended. For csv output, use the value 'csvheader' to include a
header line with field names.

.. raw:: html

   </td></tr>
   <tr><td>

envelope-template

.. raw:: html

   </td><td>

Out

.. raw:: html

   </td><td>

(template/html) the template for the envelope.

.. raw:: html

   </td></tr>
   <tr><td>

escape

.. raw:: html

   </td><td>

In/out

.. raw:: html

   </td><td>

escape character used. Default: edifact: '?'.

.. raw:: html

   </td></tr>
   <tr><td>

field\_sep

.. raw:: html

   </td><td>

In/out

.. raw:: html

   </td><td>

field separator. Default: edifact: '+'; csv: ':' x12: '')

.. raw:: html

   </td></tr>
   <tr><td>

forcequote

.. raw:: html

   </td><td>

Out

.. raw:: html

   </td><td>

(csv) Possible values: 1 (quote only if necessary); 1 (always quote), 2
(quote only alfanum). Default is 1

.. raw:: html

   </td></tr>
   <tr><td>

forceUNA

.. raw:: html

   </td><td>

Out

.. raw:: html

   </td><td>

(edifact) Always use UNA-segment in header, even if not needed. Possible
values: True, False. Default: False.

.. raw:: html

   </td></tr>
   <tr><td>

indented

.. raw:: html

   </td><td>

Out

.. raw:: html

   </td><td>

(xml, json) Indent message for human readability. Nice while testing.
Indented messages are syntactically OK, but are much bigger. Possible
values: True, False. Default: False. See also add\_crlfafterrecord\_sep

.. raw:: html

   </td></tr>
   <tr><td>

merge

.. raw:: html

   </td><td>

Out

.. raw:: html

   </td><td>

if merge is True: merge translated messages to one file (for same
sender, receiver, messagetype, channel, etc). Related: envelope.
Possible values: True, False.

.. raw:: html

   </td></tr>
   <tr><td>

namespace\_prefixes

.. raw:: html

   </td><td>

Out

.. raw:: html

   </td><td>

(xml) to over-ride default namespace prefixes (ns0, ns1 etc) for
outgoing xml. is a list, consisting of tuples, each tuple consists of
prefix and uri. Example:
'namespace\_prefixes':[('orders','http://www.company.com/EDIOrders'),]

.. raw:: html

   </td></tr>
   <tr><td>

noBOTSID

.. raw:: html

   </td><td>

In/Out

.. raw:: html

   </td><td>

(csv) use if records contain no real record ID.

.. raw:: html

   </td></tr>
   <tr><td>

output

.. raw:: html

   </td><td>

Out

.. raw:: html

   </td><td>

(template) values: 'xhtml-strict'

.. raw:: html

   </td></tr>
   <tr><td>

pass\_all

.. raw:: html

   </td><td>

In

.. raw:: html

   </td><td>

(csv, fixed) if only one recordtype and no nextmessageblock; False: pass
record for record to mapping; True: Pass all records to mapping.

.. raw:: html

   </td></tr>
   <tr><td>

quote\_char

.. raw:: html

   </td><td>

In/Out

.. raw:: html

   </td><td>

(csv) char used as quote symbol

.. raw:: html

   </td></tr>
   <tr><td>

record\_sep

.. raw:: html

   </td><td>

In/out

.. raw:: html

   </td><td>

char used as record separator. Defaults: edifact: ''' (single quote);
fixed: ''; x12: '~'

.. raw:: html

   </td></tr>
   <tr><td>

record\_sep

.. raw:: html

   </td><td>

In/out

.. raw:: html

   </td><td>

char used as record separator. Defaults: edifact: ''' (single quote);
fixed: ''; x12: '~'

.. raw:: html

   </td></tr>
   <tr><td>

record\_tag\_sep

.. raw:: html

   </td><td>

Out

.. raw:: html

   </td><td>

(tradacoms) separator used after segment tag. Defaults: '='

.. raw:: html

   </td></tr>
   <tr><td>

replacechar

.. raw:: html

   </td><td>

Out

.. raw:: html

   </td><td>

(x12) if a separator value is found in the data, replace with this
character. Default: '' (raise error when separator value in data).

.. raw:: html

   </td></tr>
   <tr><td>

skip\_char

.. raw:: html

   </td><td>

In

.. raw:: html

   </td><td>

char(s) to skip, not interpreted when reading file. Typically '' in
edifact.

.. raw:: html

   </td></tr>
   <tr><td>

skip\_firstline

.. raw:: html

   </td><td>

In

.. raw:: html

   </td><td>

(csv) skip first line (often contains field names). Possible values:
True/False/Integer number of lines to skip, default: False. True skips 1
line.

.. raw:: html

   </td></tr>
   <tr><td>

startrecordID

.. raw:: html

   </td><td>

In

.. raw:: html

   </td><td>

(fixed) start position of record ID; value: number, default 0. See
endrecordID

.. raw:: html

   </td></tr>
   <tr><td>

template

.. raw:: html

   </td><td>

Out

.. raw:: html

   </td><td>

(template) Template to use for HTML-output.

.. raw:: html

   </td></tr>
   <tr><td>

triad

.. raw:: html

   </td><td>

In

.. raw:: html

   </td><td>

triad (thousands) symbol used (e.g. '1,000,048.35'). If specified, this
symbol is skipped when parsing numbers. By default numbers are expected
to come without thousands separators.

.. raw:: html

   </td></tr>
   <tr><td>

version

.. raw:: html

   </td><td>

Out

.. raw:: html

   </td><td>

(edifact,x12) version of standard generate. Value: string, typically:
'3' in edifact or '004010' for x12.

.. raw:: html

   </td></tr>
   <tr><td>

wrap\_length

.. raw:: html

   </td><td>

Out

.. raw:: html

   </td><td>

Wraps the output to a new line when it exceeds this length. value:
number, default 0. Typically used in conjunction with
'add\_crlfafterrecord\_sep':'' (blank). Note: does not affect envelope
of message.

.. raw:: html

   </td></tr>

