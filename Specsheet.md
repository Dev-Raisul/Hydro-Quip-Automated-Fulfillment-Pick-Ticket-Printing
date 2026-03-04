# Hydro-Quip-Automated-Fulfillment-Pick-Ticket-Printing
Specsheet 

Hydro-Quip SpecificaƟon rev1
Automated Fulfillment Pick Ticket PrinƟng 1/29/2026
OBJECTIVE:
This uƟlity will generate a Crystal Reports pick Ɵcket for any unprinted pick Ɵckets for a specific
customer and will include all line items from the two warehouses servicing the customer. The
user interface will have a ‘Print’ buƩon with limited feedback along with a view of the prinƟng
log and an ability to reprint dependent upon the status of the order.
APPLICATION DETAIL:
1. Seƫngs – The seƫngs will only be accessible to workstaƟons listed in the zpt_PTSecurity
table (a new table for the applicaƟon)
a. Path and filename of the crystal report which will be used as the format for the
printed pick Ɵcket
b. Customer ID: customer number to use to filter the orders such that only orders
where the order header customer number is equal to this value
c. Reprint Password – aŌer selecƟng the ‘Reprint’ buƩon the system will prompt for
the password
2. User Interface
a. Header SecƟon –
i. General: The header will be dedicated to a large ‘PRINT NEW ORDERS’
buƩon
ii. Print AcƟon: When selected will idenƟfy the orders to be printed and
aŌer prinƟng display the number of orders that printed along with the
number of line items with item numbers that were on those orders.
iii. SelecƟon: Only orders that are less than status 4 (pick Ɵcket printed) and
that have a customer number matching that of the customer number
specified in seƫngs.
iv. Logging: Upon prinƟng, the following informaƟon will be entered into the
zPTLog table (a new table for the applicaƟon)
1. Order Number
2. Order Date
3. Print DateƟme
4. Status at Ɵme of prinƟng
5. Reprinted (yes/no)
6. Status before prinƟng
7. Reprint – always No for the first prinƟng
v. AŌer prinƟng refresh the log displayed and return to the user interface.
vi. AŌer prinƟng the order status and related ‘pick’ data will be updated
directly in the applicable SQL tables

Hydro-Quip SpecificaƟon rev1
Automated Fulfillment Pick Ticket PrinƟng 1/29/2026

b. Print Log
i. General: This secƟon will be a display of the print log along with related
current informaƟon for the order.
ii. Log SecƟon:
1. Filter - This report will only show log records for orders sƟll
exisƟng in the open order header table
2. Columns –
a. Reprint SelecƟon checkbox – the user can select this to flag
the order to reprint. This can only be selected if the order
status is 4 and there is no Tracking or Invoice number for this
order.
b. Order Number
c. Order Date
d. Print DateƟme – the date and Ɵme that this order was printed
, whether first print or re-print.
e. Status @ Print - Order Status at the Ɵme of prinƟng or
reprinƟng
f. Reprint – was this a reprint
g. Curr Status – the current status of the order – order header
status field
h. First Tracking# - the first tracking number for the order (source
from query1)
i. Invoice# - the current value of the inv_no field in the order
header
3. Reprint BuƩon – upon pressing the buƩon the following acƟons
will occur
a. Request the user to enter the Reprint password –
validaƟng the password and proceeding if the password
was correct or returning a negaƟve confirmaƟon if the
password was not correct and then returning to the user
interface without prinƟng. The following are aŌer
successful credenƟals.
b. Call the crystal pick Ɵcket printer and including the
parameter “Yes” for the Reprint
c. Enter the reprint in the log as stated above for the regular
prinƟng with the change that the reprint field will now be
“Yes”.
d. Return to the user interface and refresh the log

LimitaƟons and Exclusions:
 The applicaƟon is not mulƟ-user and intended to be run from one workstaƟon at a Ɵme
 The applicaƟon will run on Windows 10 or 11
 Operates with Version 7.x of the ERP system
 Operates with version X.XX of SQL Server
 No other funcƟons or features outside of this specificaƟon are included in the final
applicaƟon
 Thorough user tesƟng is required prior to deployment
 User is to validate that the design of the ERP table updates (change to status 4 and
related) are accurate
