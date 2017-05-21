## Filenames

In a perfect world, filenames are unimportant in the EDI
flow. All that is required is that they are unique so no file is ever
overwritten. Bots takes care of this automatically by default when
creating files, by using counters to generate unique numeric filenames.
But sometimes in the "real world" implementation of system interfaces,
you want or need to have specific filenames: 

-	 because your trading partner requires it 
-	 limitations of other systems regarding filenames 
-	 to provide easy identification of files 
-	 nicer for end users (eg. when emailing attachments)

### Input filenames

Bots uses [filename pattern
matching](http://docs.python.org/library/fnmatch.html#module-fnmatch) to
select input files. This allows you to select all files, or only
specific files, from the channel path. Some points to consider:

-   Many types of channel (eg. ftp) are case sensitive. `*`.TXT is not
    the same as `*`.txt
-   Files with and without extensions may be treated differently; `*` is
    not the same as `*`.`*`
-   for "safety" you should use a partially specified name if possible.
    This prevents accidentally picking up files that should not be
    there. eg. use ORDER`*`.TXT rather than `*`.`*` For an in-channel
    with type=file a wild-card can be used in the path.
     If directory structure is like this:
     - botssys/infile/partner1
     - botssys/infile/partner2
     - botssys/infile/partner3
     
	use path botssys/infile/`*` to read the files in all these directories.


### Output filenames

-   A unique name can be generated with an asterisk; the asterisk is
    replaced by an unique number. Eg: order`_*`.edi -\> order1.edi,
    order2.edi, order3.edi etc
-   (bots \> = 3.0) Any **ta** value can be used; eg. \`{botskey},
    {alt}, {editype}, {messagetype}, {frompartner}, {topartner},
    {fromchannel}, {tochannel}, {idroute}.
-   (bots \> = 3.0) Date/time using `{datetime}` with any valid [date or
    time format](http://docs.python.org/library/time.html#time.strftime)
    specification; eg. `{datetime:%Y%m%d}, {datetime:%H%M%S}` etc.
-   (bots \> = 3.0) Incoming filename can be used (name and extension,
    or either part separately); eg.
    `{infile}, {infile:name}, {infile:ext}`
-   **Warning:** Do not change out.ta\_info['filename'] in your scripts.
    Although it may appear to work, it messes up Bots internal file
    storage.

-   Some examples are shown in the table below.

Channel filename|Description|Example filename generated
----------------|-----------|--------------------------
`*` or blank    |create a unique name, no extension|`39724`
`*.txt`         |create a unique name with .txt extension|`39724.txt`
`{botskey}.txt` |use incoming [botskey](ConfigurationBotskey.md) value (eg. order number) with .txt extension. Note: {botskey} can only be used if merge is False for the messagetype|`BA7358-0.txt`
`{infile}`      |passthrough incoming filename & extension to output|`Order001.edi`
`{infile:name}.txt`|passthrough incoming filename but change extension to .txt|`Order001.txt`
`{editype}_{messagetype}_{datetime:%Y%m%d}_*.{infile:ext}`|use editype, messagetype, date and unique number with extension from the incoming file|`edifact_ORDERSD93AUN_20120926_39724.edi`
`{frompartner}/{editype}/{infile}`|You can also use subdirectories in the filename, but they must already exist. These will be appended to the path.|`KMART/edifact/Order001.edi`
`{frompartner}/INPUT/ORDER_{botskey}.csv`|Fixed values can also be included as part of the directory structure or filename|`KMART/INPUT/ORDER_BA7358-0.csv`
`{overwrite}daily_report.txt`|Force overwriting of a file if it exists. **Use this with caution; make sure it is really what you want!** May be required on some sftp servers that do not support append mode.|`daily_report.txt`
`{infile[4]}{infile[5]}{infile[6]}{infile[7]}.xml`|This functionality uses the Python [Format String Syntax](http://docs.python.org/2/library/string.html#formatstrings) which does not have support for "slicing", but you can use this workaround to pick a range of single characters. **Beware: this does not check for wrong string positions.**|infile: `INV_7389.txt` generates: `7389.xml`


### User scripting for output filenames

Bots has the capability to set output filenames with a
[communicationscript](ChannelsScripting.md); however this requires a new
script for each channel and is somewhat complex. Prior to version 3.0
this was the only method available. It can still be used for difficult
requirements (but let us know about your needs through the mailing list,
we may be able to integrate it).

