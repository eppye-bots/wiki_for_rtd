## Document View 
Bots focuses mostly on edi files.  
Another useful way of looking at edi is to view at 'business
documents': orders, asn's, invoices etc.

Bots support this, but to have this work satisfactory some
configuration needs to be done.  
Essential is the use of document numbers (eg order number, shipment
number, invoice number); in bots this is called 'botskey'.

### Usage

Once 'botskey' is set correct for your documents, it can be used for:

-   Viewing and searching business documents:
    -   View last run: *bots-monitor-\>Last run-\>Document*
    -   View all runs: *bots-monitor-\>All run-\>Document*
    -   Select/search for documents: *bots-monitor-\>Select-\>Document*
-   Set output [file name in a
    channel](Filenames.md) or in a
    [communicationscript](ChannelsScripting.md)


### Configure botskey

This can be done in two ways:

1.  Using QUERIES in the
    [grammar](GrammarsIntroduction.md) of
    the incoming edi file.

        # Example: botskey in a simple csv grammar
        structure = [
            {ID:'LIN',MIN:1,MAX:99999,
                QUERIES:{
                    'frompartner': ({'BOTSID':'LIN','AccountCode':None}),
                    'topartner':   ({'BOTSID':'LIN','CustomerCode':None}),
                    'botskey':     ({'BOTSID':'LIN','PurchaseOrderNo':None}),
                },
            }
        ]


2.  In your [mapping script](MappingIntroduction.md).

        out.ta_info['botskey'] = inn.get({'BOTSID':'LIN','PurchaseOrderCode':None})

