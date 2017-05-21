## High Level EDI Business Flow

Various documents need to be exchanged during the lifecycle of a business transaction.  A generic flow is shown below, this focuses on the business processes, not a particular EDI implementation (we'll get to that later).

There may be other communication, for example business process/contracts may dictate that all changes are requested and approved by email prior to the ERP systems being modified.

### Example Business Flow 

-   Buyer (customer) creates a purchase order (PO)
-   PO is sent to supplier via EDI
-   Supplier loads a Sale Order in response to the PO, with optional changes.
-   Supplier acknowledges PO (with any changes)
-   Buyer changes quantity of a line (part)
-   Buyer-initiated Change Request is sent to supplier via EDI
-   Supplier implements or rejects changes
-   Supplier sends summary of changes/rejects to buyer via EDI
-   Supplier needs to delete a line as they can no longer supply
-   Supplier sends supplier-initiated change request to buyer/customer via EDI
-   Buyer receives change request and implement or rejects changes
-   Supplier ships material
-   Supplier sends an [Advance Ship Notice](TutorialAdvanceShipNotice.md) (shipping manifest) via EDI
-   Supplier sends invoice via EDI