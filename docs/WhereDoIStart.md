## Introduction

You have been asked to integrate with other companies using EDI with a ridiculous deadline.  You have never used EDI, nor has anyone in your company.  Can you do it?  Yes, with BOTS you can.  But first there are some speed bumps that need to be cleared.

I am writing this document from the perspective I had when I spun up on BOTS and EDI.  To this end, much of this information is presented from my narrow perspective.  With time and contributions, it may be corrected, but for now it should still accomplish its primary purpose which is to prepare you for the possible carnage ahead.

### EDI? 

EDI is for data transfer.  The general idea behind EDI is to put data into electronic documents that are so standardized that you can just send them off willy nilly to any partner without any worry about mis-interpertation.  Except of course **people** decide how EDI documents get translated into and out of any computer system.  Everyone is different, and you will find that every partner will have a slightly different interpretation of what the 3 or 4 word description of each data item actually means.

EDI is old.  Unless you have been programming for a long time (mainframe?), it probably doesn't have much to do with what you know about data interchange or programming languages.  If you have done a lot of work with binary storage formats, you might be in for a treat.

EDI has many flavors.  Find out exactly what document standard you are using, and make sure you setup your tools appropriately.

EDI is insanely general.  Try to communicate with the EDI experts from your business partners.  Ask them what fields are really important.  It is not uncommon to receive hundreds of pages of documentation grandly entitled _XXX Inc Official EDI Documentation Version 1.17_ and only need to save off 7 fields from each incoming document.

EDI is closed.  For example, if you visit X12.org, don't expect any information for free.  There are however some workarounds.  If your documentation at hand for a specific piece of data is too vague, you can try googling the standard name, the document number, and the segment name.  You will usually be rewarded with many many other companies' crap documents, and sometimes with a little luck enough cross referencing can reward you with an answer.

### AS2?

It seems likely that if you are asked to deal with EDI, you will also have to deal with AS2.  AS2 is simply a secure transport mechanism.  Nothing too silly.  It does however fairly literally digitize the real world notion of INBOX and OUTBOX, presumably because it is an old standard.

Without going to far into details, AS2 uses public key encryption to encrypt a packet of data (containing an EDI file) and then signs the encrypted packet with the sender's key.

### BOTS? 

BOTS is a


### Details 

Add your content here.  Format your content with:
-	Text in **bold** or _italic_
-	Headings, paragraphs, and lists
-	Automatic links to other wiki pages
