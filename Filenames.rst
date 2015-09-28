Filenames
=========

In a perfect world, filenames are unimportant in the EDI flow. All that
is required is that they are unique so no file is ever overwritten. Bots
takes care of this automatically by default when creating files, by
using counters to generate unique numeric filenames.

But sometimes in the "real world" implementation of system interfaces,
you want or need to have specific filenames: \* because your trading
partner requires it \* limitations of other systems regarding filenames
\* to provide easy identification of files \* nicer for end users (eg.
when emailing attachments)

.. raw:: html

   <h3>

Input filenames

.. raw:: html

   </h3>

Bots uses filename pattern matching to select input files. This allows
you to select all files, or only specific files, from the channel path.
Some points to consider:

.. raw:: html

   <ul><li>

Many types of channel (eg. ftp) are case sensitive. \ *.TXT is not the
same as *\ .txt

.. raw:: html

   </li><li>

Files with and without extensions may be treated differently; \ * is not
the same as *\ .\*

.. raw:: html

   </li><li>

for "safety" you should use a partially specified name if possible. This
prevents accidentally picking up files that should not be there. eg. use
ORDER\ *.TXT rather than *\ .\ * For an in-channel with type=file a
wild-card can be used in the path. If directory structure is like this:
- botssys/infile/partner1 - botssys/infile/partner2 -
botssys/infile/partner3 use path botssys/infile/*\  to read the files in
all these directories.

.. raw:: html

   </li></ul>


.. raw:: html

   <h3>

Output filenames

.. raw:: html

   </h3>
   <ul><li>

A unique name can be generated with an asterisk; the asterisk is
replaced by an unique number. Eg: order\_\*.edi -> order1.edi,
order2.edi, order3.edi etc

.. raw:: html

   </li><li>

(bots > = 3.0) Any ta value can be used; eg. \`{botskey}, {alt},
{editype}, {messagetype}, {frompartner}, {topartner}, {fromchannel},
{tochannel}, {idroute}.

.. raw:: html

   </li><li>

(bots > = 3.0) Date/time using {datetime} with any valid date or time
format specification; eg. {datetime:%Y%m%d}, {datetime:%H%M%S} etc.

.. raw:: html

   </li><li>

(bots > = 3.0) Incoming filename can be used (name and extension, or
either part separately); eg. {infile}, {infile:name}, {infile:ext}

.. raw:: html

   </li><li>

Warning: Do not change out.ta\_info['filename'] in your scripts.
Although it may appear to work, it messes up Bots internal file storage.

.. raw:: html

   </li></ul>

   <ul><li>

Some examples are shown in the table below.

.. raw:: html

   </li></ul>

   <table><thead><th> 

Channel filename

.. raw:: html

   </th><th> 

Description

.. raw:: html

   </th><th> 

Example filename generated

.. raw:: html

   </th></thead><tbody>
   <tr><td>

\* or blank

.. raw:: html

   </td><td>

create a unique name, no extension

.. raw:: html

   </td><td>

39724

.. raw:: html

   </td></tr>
   <tr><td>

\*.txt

.. raw:: html

   </td><td>

create a unique name with .txt extension

.. raw:: html

   </td><td>

39724.txt

.. raw:: html

   </td></tr>
   <tr><td>

{botskey}.txt

.. raw:: html

   </td><td>

use incoming botskey value (eg. order number) with .txt extension. Note:
{botskey} can only be used if merge is False for the messagetype

.. raw:: html

   </td><td>

BA7358-0.txt

.. raw:: html

   </td></tr>
   <tr><td>

{infile}

.. raw:: html

   </td><td>

passthrough incoming filename & extension to output

.. raw:: html

   </td><td>

Order001.edi

.. raw:: html

   </td></tr>
   <tr><td>

{infile:name}.txt

.. raw:: html

   </td><td>

passthrough incoming filename but change extension to .txt

.. raw:: html

   </td><td>

Order001.txt

.. raw:: html

   </td></tr>
   <tr><td>

{editype}*{messagetype}*\ {datetime:%Y%m%d}\_\*.{infile:ext}

.. raw:: html

   </td><td>

use editype, messagetype, date and unique number with extension from the
incoming file

.. raw:: html

   </td><td>

edifact\_ORDERSD93AUN\_20120926\_39724.edi

.. raw:: html

   </td></tr>
   <tr><td>

{frompartner}/{editype}/{infile}

.. raw:: html

   </td><td>

You can also use subdirectories in the filename, but they must already
exist. These will be appended to the path.

.. raw:: html

   </td><td>

KMART/edifact/Order001.edi

.. raw:: html

   </td></tr>
   <tr><td>

{frompartner}/INPUT/ORDER\_{botskey}.csv

.. raw:: html

   </td><td>

Fixed values can also be included as part of the directory structure or
filename

.. raw:: html

   </td><td>

KMART/INPUT/ORDER\_BA7358-0.csv

.. raw:: html

   </td></tr>
   <tr><td>

{overwrite}daily\_report.txt

.. raw:: html

   </td><td>

Force overwriting of a file if it exists. Use this with caution; make
sure it is really what you want! May be required on some sftp servers
that do not support append mode.

.. raw:: html

   </td><td>

daily\_report.txt

.. raw:: html

   </td></tr>
   <tr><td>

{infile[4]}{infile[5]}{infile[6]}{infile[7]}.xml

.. raw:: html

   </td><td>

This functionality uses the Python Format String Syntax which does not
have support for "slicing", but you can use this workaround to pick a
range of single characters. Beware: this does not check for wrong string
positions.

.. raw:: html

   </td><td>

infile: INV\_7389.txt generates: 7389.xml

.. raw:: html

   </td></tr></tbody></table>

.. raw:: html

   <h3>

User scripting for output filenames

.. raw:: html

   </h3>

Bots has the capability to set output filenames with a
communicationscript; however this requires a new script for each channel
and is somewhat complex. Prior to version 3.0 this was the only method
available. It can still be used for difficult requirements (but let us
know about your needs through the mailing list, we may be able to
integrate it).
