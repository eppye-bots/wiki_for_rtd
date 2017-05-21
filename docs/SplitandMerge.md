## Splitting and merging edi files

### Introduction

It would be easiest if one edi-file always contains one message (eg one order). But
this is not always the case, eg: 

-	in edifact or x12 traditionally multiple messages are 'enveloped'. 
	(there was a time this was less expensive to send over networks). 
    For some VAN's this is still true. 
-	use of multiple envelopes in a file. Maybe they shouldn't do this, but
	they do. 
-	the export routine of your ERP software puts all exported
	invoices in one file So Bots has to split up edi-files, and has to be
	able to envelope and merge edi-files.
    
This wiki page gives an overview of all the possible splitting and
merging in Bots.


### Splitting

-   Incoming email: different attachments are saved as a separate
    edi-files.
-   Receiving zipped edi files: the files in the zip-file as saved as
    separate edi-files.
-   For edifact, x12, tradacoms: interchanges are being split up to
    separate files.
-   Incoming edi-files are being fed to the mapping-script as messages.
    This is done by 'nextmessage' in the grammar syntax, see
    [Nextmessage](GrammarsNextmessage.md).
-   Spit within a mapping script. Think of eg splitting up a shipment to
    the different orders. There are 2 ways of doing this:
    1.  Write multiple message to the same file.
    2.  Write each generated message to the same file, using alt
        translations.

### Merging

-	Merging: if the 'merge' parameter is set in the syntax of the outgoing
	message, bots will try to merge the separate messages to one file.
	Messages are only merged if: same from-partner, same to-partner, same
	editype, same messagetype, same testindicator, same characterset, same
	envelope.

-	Enveloping: (edifact, x12, tradacoms) bots will envelope these messages
	(add UNB-UNZ for edifact, ISA-GS-GE-IEA for x12). Enveloping is
	independent from merging: bots can envelope without merging, or merge
	without enveloping.

-	Write to a message-queue in outgoing channel: if you use a fixed
	filename in an outgoing channel, bots will append all messages to this
	file. This is often used in eg a set-up where all orders go to one file
	containing all incoming orders in fixed file format.

