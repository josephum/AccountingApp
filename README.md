CONTAPLUS

 
1. Introduction  
1.1 Scenario  
●	“Company X” needs a web based application to manage accounting tasks such  as:  
○ Sales,   
○ Purchase,  
○ Stock management,  
○ Administrative operations.   
●	A Software Development Company “CYDEO” provides such capabilities with a webbased accounting application with yearly subscriptions.   
●	When Company X pays for first month subscription, an ADMIN username and password is provided. 
●	With the provided credentials ADMIN of Company X can create MANAGER and EMPLOYEE users and Company X can keep the track of accounting processes.  
●	Company Y, Z and many others might follow the same track for their needs as well. 
 
Task: You are a software developer working for “CYDEO”. Design a web-based Accounting App for companies like “Company X” with capabilities defined in the following paragraphs.  
1.2 Purpose of Document  
This is a Requirements Specification document for a new web-based accounting system for Cydeo School Graduation Project. In the market there is a need for a new web-based accounting system.  
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
 
 
EMPLOYEE:  
 
●	CRUD of Invoices  
●	Display Stock report  
 
 
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
2. System Architecture & Business Logic  
 
 
 
 
 
 
3. The Use Case Model  
3.1. Use Case Descriptions (for selected cases)  
•	For all use cases, the user can cancel the use case at any step that requires user input. This action ends the use case. Any data collected during that use case is lost.  
•	For all use cases that require a logged in user, the current login session is updated during the use case to reflect the navigation paths through the use case.  
Login User 
Use Case   	Login User  Name:  
Summary:  To get personalized or restricted information, place orders or do other specialized transactions a user must login so that that the system can determine his access level.  
	Basic Flow:  	1. The use case starts when a user indicates that he wants to login.  
2.	The system requests the username and password.  
3.	The user enters his username and password.  
4.	The system verifies the username and password against all registered users.  
5.	The system starts a login session and displays a welcome message based on the user's preferences.  
	Alternative   	 
	Flows:  	1. If username is invalid, the use case goes back to Login 
2. If the password is invalid the system requests that the user re-enter the password. When the user enters another password the use case continues with using the original username and new password.  
 
	Extension   	None  
Points:  
 
The user is registered.  
Preconditions:  
Postconditions: The user can now obtain data and perform functions according to his registered access level.  
Business Rules: Some data and functions are restricted to certain types of users or users with a particular access level. 
Register User (ROOT, ADMIN) 
 
Use Case Name: To get personalized or restricted information, place invoice or do other Register 	User specialized operations a new user must register a username and Summary:  	password.  
 
1.	The use case starts when a user indicates that he wants to register. 
Basic Flow:  
2.	The system requests a username and password.  
3.	The user enters a username and password.  
4.	The system checks that the username does not duplicate any existing registered usernames.  
5.	The system requests a first name, last name, email, password, company, and access level.  6. The user enters the information.  
7.	The system determines the user's access level and stores all user information.  
8.	The system executes use case Dashboard Population.  
9.	The system starts a login session and displays a welcome message based on the user's preferences.  
Alternative   
Flows:  • Step 1: If the username duplicates an existing username the system displays a message, and the use case goes back.  
• Step 2: If the user does not enter a required field, a message is displayed, and the use case repeats step 1.  
 	 
 
	Extension   	none  
Points:  
 	 
Preconditions: The user can now obtain data and perform functions according to his Postconditions:  registered access level. 
 
 
 
 
 
 
 
 
Register Company (ROOT) 
 
	Summary:  	Use Case Name: Register Company  
To place invoice, sell/purchase product, register user and generate 
	 	reports new company must be registered with proper information  
 
Basic Flow:  
1.	The use case starts when a user indicates that he wants to register company.  
2.	The system requests a company title.  
3.	The system requests a company address  
4.	The system requests a state, zip and representative  
5.	The system requests a company email  
6.	The system requests a company establishment date  
7.	The system checks that the company title does not duplicate any existing registered company.  
8.	The user enters the information.  
9.	The system executes use case Register User.  
10.	The system starts a login session and displays a welcome Alternative   message based on the user's preferences.  Flows:  
•	Step 1: If the company title duplicates an existing company the system displays a message, and the use case goes back.  
•	Step 2: If the user does not enter a required field, a message is 
	 	displayed, and the use case repeats step 2.  
 
Extension   
	Points:  	none  
 
 	 
	Preconditions:  	The user can now use accounting application properly 
  
 
 
 
 
 
 
 
 
Dashboard Population (ADMIN, MANAGER, EMPLOYEE) 
Use Case   	Dashboard Population  Name:  
	Summary:  	This use case allows a registered user to land in main page and see 
annual statistics, stock condition and currency exchange information.  
	Basic Flow:  	1. The use case start when a user logs in the web application  
2.	The system displays all invoices per year by count on the left side of 
	 	the page  
3.	The system displays stock condition per product  
	Alternative 	 
Flow: 1. Some restriction might be applied if qty less than 5 row can be  colored with red or else green  
	 	2. The system displays current exchange rates in euro, yen, rupi   
	Extension   	 
	Points:  	None  
 
Preconditions: The user is logged in. 
Place Purchase Invoice (MANAGER, EMPLOYEE) 
Summary:  	Use Case Name: Place Purchase Invoice  Scenario: User places invoice.  
Basic Flow:  This use case allows a registered user to place an invoice for a vendor  	or customer.  
 1. The use case starts when a user indicates he wants to place an  invoice for the current vendor or customers with existing products   2. The system displays the products information: name  
3.	The system requests the quantity to order.  
 
4.	The system requests the price per product  
 
5.	The system allows add/remove multiple product item per invoice  
 
6.	The user may add or change any of the information.  
 
7.	The system stores the invoice information, decreases the quantity 
 on hand for the product.  
 
8.	The system displays an order completion message and sends a 
 receipt to the user.  Extension   
	Points:  	None 
 
Preconditions: The customer is logged in and has requested to create purchase Postcondition:  invoice The product is bought. 
List Purchase Invoice (MANAGER, EMPLOYEE) 
	Summary:  	Use Case Name: Place Purchase List  
Scenario: User displays purchase invoice list.  
Basic Flow:  	This use case allows a registered user to display a list of purchase  	invoices. 
1.	The use case starts when a user indicates he wants to display a 
	 	purchase invoice  
2.	The system displays the purchase invoices with the information  	below.  
a.	invoice no,  
 
b.	vendor name,  
 
c.	total price,  
 
d.	invoice date   
 
3.	The system displays an invoice within the table format. 
 
 
Extention 
none  
Points:  
 
Preconditions: 
The customer is logged in and has requested to display purchase 
Postcondition:  invoice list the purchase invoices have been listed 
Place Sales Invoice (MANAGER, EMPLOYEE) 
Summary:  	Use Case Name: Place Sales Invoice   	Scenario: User places invoice.  
 	This use case allows a registered user to place an invoice for a  	customer.  
Basic Flow:  1. The use case starts when a user indicates he wants to place an  invoice for the current customers with existing products  
2.	The system displays the products information: name  
3.	The system requests the quantity to sell.  
 
4.	The system requests the price&tax per product  
5.	The system allows add/remove multiple product item per invoice  
6.	The user may add or change any of the information.  
7.	The system stores the invoice information, decreases the quantity on hand for the product.  
 
	Extension   	None 
Points:  
 
The customer is logged in and has requested to create sales invoice Preconditions: for sold products.  
Postcondition:  If the quantity on hand is not sufficient for this order, a message is sent to the user the use case is canceled. 
Sales Invoice List (MANAGER, EMPLOYEE) 
	Use 	Case Scenario: User displays sales invoice list.  
	Name: 	Place This use case allows a registered user to display a sales invoices. 
	Sales 	List 
 
Summary:  
Basic Flow:  1. The use case starts when a user indicates he wants to display a purchase invoice   
2.	The system displays the purchase invoices with the information below;  
a.	invoice no,  
b.	customer name,  
c.	total price,  
d.	invoice date   
e.	the user who created purchase invoice  
3.	The system displays an invoice within the table format sorted by 
	Extension   	date. none  
	Points:  	 
Preconditions: The customer logged in and has requested to display sales invoice list Postcondition:  The purchase invoices have been listed 
Register Product Category (MANAGER) 
	Summary:  	Use Case Name: Place Product Category  
	Basic Flow:  	Scenario: User registers a product category for a company  
	 	This use case allows a registered user to place new product category  
1.	The use case starts when a user indicates he wants to register a product category  
 
2.	The system requests below information to create new category.  
	 	a. Category name  
3.	The system completes the registration. 
4.	If the category name duplicates an existing category name for the company the system displays a message, and the use case goes back 
 to step 2. 
5.	If the user does not enter a required field, a message is displayed,  and the use case repeats step 2.  
	Extension 	None  
Points: 
 The customer is logged in and has requested to place product category Preconditions: The product category has been created Postcondition:  
 
 
 
Register Product (MANAGER) 
 
 
 
 
 
 
 
 
 
 
 
 
Register Vendor/Client Companies (MANAGER) 
 
	Summary:  	Use Case Name: Place New 3r party companies   
Scenario: User registers a vendor or customer companies  
Basic Flow:  This use case allows a registered user to place new 3rd party companies to fulfill sales or purchase invoices  
1.	The use case starts when a user indicates he wants to register a new 3rd party company   
2.	The system requests below information to create new 3rd party companies.  
a.	Company name  
b.	phone  
c.	email  
Alternative   
d.	address Flows:  
e.	state 
 
f.	zip code  	rd party company types: Vendor, Client  
3.	The system displays the 3
 
4.	If the name duplicates an existing company name for the 3rd party  company the system displays a message, and the use case goes back 
	 	to step 2  
 
5.	If the user does not enter a required field, a message is displayed,  and the use case repeats step 2.  
	Extension   	None  
Points:  
Preconditions: The user is logged in and has requested to place a vendor or customer 
Postcondition:  The 3rd party company has been created 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
Display Stock Status (MANAGER, EMPLOYEE) 
 
 
 
 
 
 
 
 
 
 
 
 
 
Generate Profit & Loss Report (MANAGER) 
 
 
 
 
 
 
 
 
 
 
 
4. Mock User Interface Design  
 
4.3 Management Menu  
 
 
 
4.6 User Registration Menu-List of Users 
 
    
4.8 Client/ Vendor Registration Menu-List of Client/Vendors 
 
 
 
 
 
 
 
 
4.10 Stock Management Menu  
 
 
 
 
 
 
 
4.12 Stock Management Menu – Add Product  
 
 
 
 
 
4.17-1 Invoices Menu – Purchase Invoice – To Invoice 
 
 
 
 
4.19 Invoices Menu – Purchase Invoice – Add Invoice Product 
 
  
 
 
 
 
 
 
 
 
 
 
 
 
 
4.23 Administration Menu 
 
 
 
 
 
 
4.25 Administration Menu – Invoice 
 
 
 
 
 
 
 
 
 
5. Database Design (E-R Diagram) 
 
![image](https://user-images.githubusercontent.com/39348176/185193169-04447477-258b-4c31-a037-f185607a2299.png)
