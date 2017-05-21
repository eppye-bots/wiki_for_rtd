## Channels Introduction

Channels take care of communication: file I/O, ftp, email, etc.
A channel is either incoming or outgoing.  
Examples of channels:

-   receive email from a pop3-mailbox
-   send to a ftp-server
-   pick up in-house invoices from a directory on your computer
-   put orders in a file queue for import in your application.

> Example of communication channels for bots:
>  ![](ChannelScheme.png)

Notes on naming conventions:

-   incoming = incoming to bots
-   outgoing = going out bots
-   inbound = my organization receives
-   outbound = going out of my organization


 Note: Bots does client communicates (no server). If you need a
communication server (eg for ftp, as2), use a separate server.

