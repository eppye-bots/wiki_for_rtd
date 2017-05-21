## How translations work

Best understood by looking at this schema:  

![MappingScheme.png](MappingScheme.png)

Step-by-step:

1.	The edi file is lexed and parsed using the
	[grammar](GrammarsIntroduction.md).

2.	The message is transformed into a tree structure. This is similar to the
	use of DOM in xml. Advantages:
	-   easy access to message content. This is quite similar to XML-queries
    	or X-path.
	-   choose the logic for the mapping script that is best fit for the
    	situation - instead of being forced to 'loop' over incoming
    	message.
	-   Sorting: eg. sort article lines by article number.
	-   Counting: eg. count number of lines, total amounts etc
	-   Access the data you already written in the tree

[Split](ConfigurationSplit.md) the edi file into separate messages (eg
one edi file can contain multiple orders).

Find the [right translation](TranslationRules.md) for message.

Run the [mapping script](MappingIntroduction.md) for message.

Serialize the outmessage-tree to file. This is checked and formatted
according to the [grammar](GrammarsIntroduction.md) of the outgoing
message.

Outgoing messages are [enveloped and/or merged](ConfigurationMerge.md).

