OBJECTIVE:
This utility will generate a Crystal Reports pick ticket for any unprinted pick tickets for a specific customer and will include all line items from the two warehouses servicing the customer.  The user interface will have a ‘Print’ button with limited feedback along with a view of the printing log and an ability to reprint dependent upon the status of the order.
APPLICATION DETAIL:
1.	Settings – The settings will only be accessible to workstations listed in the zpt_PTSecurity table (a new table for the application)
a.	Path and filename of the crystal report which will be used as the format for the printed pick ticket
b.	Customer ID: customer number to use to filter the orders such that only orders where the order header customer number is equal to this value
c.	Reprint Password – after selecting the ‘Reprint’ button the system will prompt for the password
2.	User Interface
a.	Header Section – 
i.	General: The header will be dedicated to a large ‘PRINT NEW ORDERS’ button 
ii.	Print Action: When selected will identify the orders to be printed and after printing display the number of orders that printed along with the number of line items with item numbers that were on those orders.
iii.	Selection: Only orders that are less than status 4 (pick ticket printed) and that have a customer number matching that of the customer number specified in settings.
iv.	Logging: Upon printing, the following information will be entered into the zPTLog table (a new table for the application)
1.	Order Number
2.	Order Date
3.	Print Datetime
4.	Status at time of printing
5.	Reprinted (yes/no)
6.	Status before printing
7.	Reprint – always No for the first printing
v.	After printing refresh the log displayed and return to the user interface.
vi.	After printing the order status and related ‘pick’ data will be updated directly in the applicable SQL tables


b.	Print Log
i.	General: This section will be a display of the print log along with related current information for the order.
ii.	Log Section: 
1.	Filter - This report will only show log records for orders still existing in the open order header table
2.	Columns – 
a.	Order Number
b.	Order Date
c.	Print Datetime – the date and time that this order was printed , whether first print or re-print.
d.	Status @ Print - Order Status at the time of printing or reprinting
e.	Reprint – was this a reprint
f.	Curr Status – the current status of the order – order header status field
g.	First Tracking# - the first tracking number for the order (source from query1)
h.	Invoice# - the current value of the inv_no field in the order header
3.	Reprint – the user will highlight one order and either right click or choose the reprint button.
a.	Right click the order to reprint – brings up an option to reprint the order
b.	Button – upon pressing the button the following actions will occur
c.	Request the user to enter the Reprint password – validating the password and proceeding if the password was correct or returning a negative confirmation if the password was not correct and then returning to the user interface without printing.  The following are after successful credentials.
d.	Call the crystal pick ticket printer and including the parameter “Yes” for the Reprint
e.	Enter the reprint in the log as stated above for the regular printing with the change that the reprint field will now be “Yes”.
f.	Return to the user interface and refresh the log
 
APPENDIX
Draft Application Interface:
 
Note that although the functionality and function of the screens presented will not change the final layout/design may be different
Limitations and Exclusions:
•	The application is not multi-user and intended to be run from one workstation at a time
•	The application will run on Windows 10 or 11
•	Operates with Version 7.x of the ERP system
•	Operates with version X.XX of SQL Server
•	No other functions or features outside of this specification are included in the final application
•	Thorough user testing is required prior to deployment
•	User is to validate that the design of the ERP table updates (change to status 4 and related) are accurate
