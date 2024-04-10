# Merge Syncro Ticket Timers

This flow has been tested in my environment and will require changes to work in yours, I suggest thoroughly testing before going live.

This is a power automate flow that runs hourly to find any tickets of the status Ready To Bill, it collects all billable line items and merges them in to a single charge for each labour type.
The sample here has 4 labour types defined but you can replicate the sections of the flow to add as many as you like.

Update the variables Initialize SyncroDomain and Initialize SyncroAPIKey with your own values
Update the Switch Cases with the Product ID for the respective labour types, also update the HTTP - Add Line Item steps with the matching Product IDs

On a small ticket, with only a few time entries the runtime of the flow is around 15 seconds per ticket.
This flow does not take in to account pagination of the initial Ready To Bill tickets list so will only process 50 tickets per run. This is sufficient for my needs by feel free to adapt if you need more.

Syncro API Permissions Required:
Ticket Timers - Overview
Tickets - Edit Single-Customer
Tickets - List/Search Single-Customer

The flow also send a Teams chat message after each ticket is processed to allow easy checking of processed tickets, this is no essential to the flow but recommended.

Although there is a Delete Line Items step at the end this appears to leave the Labour Log items in their original state (Charged or Not Charged), if somehting goes wrong you can clear the charges in re-charge in the labour log to reinstate the original charges.

Due to rounding issues, the final labour charge on the consolidated items may be a minute or two higher or lower than the split line items; this will be fixed in a later release of the flow.
