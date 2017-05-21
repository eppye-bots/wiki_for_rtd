## Merge/envelope edi message

Reasons to merge/envelope edi files: 

-	your ERP-system expects one file (message-queue) with fixed
	records 
-	your edi-partners wants to limit the number of
	edi-files/interchanges received. 
-	costs: this can reduce transmission
	costs for some VAN's 
-	It is better to have one file with outgoing
	invoices than 165 separate files ;-)
    
Merge options:

-	Merging: if the 'merge' parameter is set in the syntax of the outgoing
	message, bots will try to merge seperate messages to one file. Messages
	are only merged if: same from-partner, same to-partner, same editype,
	same messagetype, same testindicator, same characterset, same envelope.
    
-	Enveloping: (edifact, x12, tradacoms) bots will envelope these messages
	(add UNB-UNZ for edifact, ISA-GS-GE-IEA for x12). Enveloping is
	independent from merging: bots can envelope without merging, or merge
	without enveloping.
    
-	Write to a message-queue in outgoing channel: if you use a fixed
	filename in an outgoing channel, bots will append all messages to this
	file. This is often used in eg a configuration where all orders go to
	one file containing all incoming orders in fixed file format.
