CONTAPLUS

1. Introduction  
1.1 Scenario  
●	“Company X” needs a web based application to manage accounting tasks such  as:  
○ Sales,   
○ Purchase,  
○ Stock management,  
○ Administrative operations.   
●	A Software Development Company “JOSEPHUM INC” provides such capabilities with a webbased accounting application with yearly subscriptions.   
●	When Company X pays for first month subscription, an ADMIN username and password is provided. 
●	With the provided credentials ADMIN of Company X can create MANAGER and EMPLOYEE users and Company X can keep the track of accounting processes.  
●	Company Y, Z and many others might follow the same track for their needs as well. 
 
Task: You are a software developer working for “JOSEPHUM INC”. Design a web-based Accounting App for companies like “Company X” with capabilities defined in the following paragraphs.  


1.2 Purpose of Document  
This is a Requirements Specification document for a new web-based accounting system. In the market there is a need for a new web-based accounting system.  
The accounting application will operate below main capabilities: 
●	Create users with ROOT, ADMIN, MANAGER, and EMPLOYEE roles 
●	ADMIN user will crud companies, clients, and vendors 
●	ROOT user will crud companies and ADMIN user for the company 
●	ADMIN user will crud MANAGERs and EMPLOYEEs for his/her company 
●	MANAGERs will crud categories and products 
●	MANAGERs and EMPLOYEEs will crud invoices (purchase or sales)  ● MANAGERs will generate stock-based reports. 
●	MANAGER will pay application monthly usage fee for the application ● Aforementioned processes will be managed under separate companies  ● This will be a Software as a Service (SAAS).   

1.3 Project Scope  
The scope of this project is a web-based system that supports the accounting operations of SMC. The web site will support major accounting operations like sales, purchase and stock management as well as administrative operations.

1.4 System Purpose

1.4.1 Users

Those who will primarily benefit from the new system and those who will be affected
by
the new system include
Upon implementation of the accounting system, root users has below functionalities:
● Crud companies
● Assign ADMIN type users for the companies.
ADMIN:
The admin user has two main functionalities:
● Crud MANAGERs and/or EMPLOYEEs
MANAGER:
Managers have several capabilities to operate the web site to achieve accounting processes:
● Crud of categories and products
● Crud of 3rd party Client/Vendor companies
● Crud and Approval for Invoices
● Generate stock and profit-loss report
● Pay monthly usage fee of application
EMPLOYEE:
● CRUD of Invoices
● Display Stock report
 
 
1.4.2 Responsibilities  
The primary responsibilities of the new system:  
●	Main dashboard should have below statistics by company  
○	Total purchase invoice amount of current year  
○ Total sales invoice amount of current year   
○ Total profit/loss of current year 
○ Currency information. 3rd party API will be consumed via WebClient  ● Management module should have below functionality: 
○ There should be 2 main sub-modules, one for User CRUD, one for Client/Vendor Crud 
○ Admin must have the only authority to create new MANAGER and EMPLOYEE ○ All User information should be SECURE and CYRPTED. 
●	Stock Management module should have below functionality: 
○	Stock management should be done via Queue (logic only) implementation. 
○ First product purchased should be sold first ○ Profit calculation should be based on this criterion. 
●	Invoice module should have below functionality: 
○	There should be two sub-modules (Purchase and Sales) which must have all CRUD operations 
○ When selected all invoices should be listed in the list invoice page ● Invoice – stock relation will be handled automatically.  
○ If the purchase invoice is saved, stock quantity should be increased automatically.   
○ If the sales invoice saved, it will need an extra approval for stock quantity be decreased. 
○ If there is not enough product in the stock this product should not be added to invoices. 
○ If there is not enough product in the stock invoice should not be approved 
●	Total profit or loss should be calculated based on purchase vs sales prices ○ Total profit will be calculated by product price, amount, and tax.  
○	FIFO approach should be used. The first product entered stocks will be sold first. 
And the profit/loss for this product will be calculated based on these computations.   
●	Menu should be populated by user credentials.  
●	Each service should you logged using Log4j2 and daily base log file must be rolled