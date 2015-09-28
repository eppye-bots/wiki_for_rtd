Archiving of EDI files
----------------------

The current archive
~~~~~~~~~~~~~~~~~~~

Bots always uses the current archive. The current archive is what can be
seen in the bots-monitor: incoming files, outgoing files, document view
etc. Edi-files are kept 30 days in the current archive (by default, can
be set via parameter maxdays in bots/config/bots.ini). After this time
the edi-files and data about their processing (like runs, incoming
files, etc) are discarded.

.. raw:: html

   <h3>

Discussion about long term archiving

.. raw:: html

   </h3>

How long should edi-files be archived? There is no fixed rule about
this. Some argue that the edi-files are temporary information carriers
and that the real data is processed and archived in the ERP software of
you and your edi-partner. But:

.. raw:: html

   <ul><li>

for eg invoices there might be legal issues about keeping the 'original
invoice'. Check this! (OTOH I get a big smile thinking of legal/tax
people wading though these EDI-files. ;-))

.. raw:: html

   </li><li>

it might be needed to keep the original in case there are any errors or
discrepancies that need to be investigated later.

.. raw:: html

   </li></ul>

The (default) 30 days of the current archive is a compromise between
'keep all data always' and performance. If all data are kept,
performance will degrade in the long run.

.. raw:: html

   <h3>

The long term archive

.. raw:: html

   </h3>

Bots has an option for a long term archive. how this works:

.. raw:: html

   <ul><li>

Per channel: if you specify the 'Archive path' in a channel, all files
coming in or going out for that channel are archived.

.. raw:: html

   </li><li>

for incoming files: archived as received (unchanged); for emails the
(un-mimified) attachments are saved.

.. raw:: html

   </li><li>

for outgoing files: archived as send (unchanged). If outgoing
communication fails: nothing is send, so nothing is archived.

.. raw:: html

   </li><li>

The long term archive contains copies of the files only. Once bots has
cleaned details from it's database you will need to use tools like
'grep' to find what you need.

.. raw:: html

   </li><li>

Bots creates a sub-directory per date, eg. myarchive\_path/20131202,
myarchive\_path/20131203, etc. The sub-directories contains the
edi-files archived in that day.

.. raw:: html

   </li><li>

Within this daily directory, Bots uses unique numeric filenames by
default.

.. raw:: html

   </li><li>

Edi-files are kept 180 days in the long term archive (by default, can be
set via parameter maxdaysarchive in bots/config/bots.ini). Keeping files
longer will not affect performance significantly. Of course the files
will occupy disc space.

.. raw:: html

   </li></ul>

.. raw:: html

   <h3>

Example of archiving

.. raw:: html

   </h3>

Archive path for channel my\_inchannel is set to
C:/edi/archive/my\_inchannel. Archive path for channel my\_outchannel is
set to C:/edi/archive/my\_outchannel.

After a few days this will looks someting like:

.. raw:: html

   <pre><code>C:/edi/archive/<br>
                 my_inchannel/<br>
                             20131202/<br>
                                     13892848<br>
                                     13892872<br>
                                     13892876<br>
                             20131203/<br>
                                     13892991<br>
                                     13893009<br>
                             20131204/<br>
                                     13893421<br>
                 my_outchannel/<br>
                             20131202/<br>
                                     13892861<br>
                                     13892886<br>
                             20131203/<br>
                                     13893123<br>
                             20131204/<br>
                                     13893479<br>
   </code></pre>

Note: it is strongly advised to archive the file outside of the bots
directories!

.. raw:: html

   <h3>

Additional options for long term archive

.. raw:: html

   </h3>
   <ul><li>

archiveexternalname (setting in bots/config/bots.ini). If set to True,
name of archived file is the name of the incoming/outgoing file. If this
name already exists in the archive: a timestamp is added to the
filename; eg. order.txt becomes order\_112506.txt. External filenames
are only used for some channel types where the channel defines the
filename (file, ftp, ftps, ftpis, sftp, mimefile, communicationscript).
Default setting in bots.ini is False. New in version 3.0.

.. raw:: html

   </li><li>

archivezip (setting in bots/config/bots.ini). If set to True, each
archive folder will be a zip file. If you keep archives for a long time,
zipping them can save a lot of disc-space; most EDI files compress to
just a few percent of original size. Disadvantage: harder to search.
Default setting is False. New in version 3.0.

.. raw:: html

   </li><li>

user scripting for archive path. See communicationscript. Note: please
archive within the archive path as set in channel, else the cleanup
routines for parameter maxdaysarchive will not function.

.. raw:: html

   </li><li>

user scripting for name of archive file. See communicationscript.
