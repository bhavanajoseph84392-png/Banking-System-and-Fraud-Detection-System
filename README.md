# Banking-and-Fraud-Detection-System

Overview
The Banking System Database is a MySQL project that models core banking data, including customers, bank accounts, cards, and financial transactions. It demonstrates relational database design and SQL querying for retrieving, filtering, summarizing, and joining banking records.
Objectives
- Organize banking data into related tables.
- Enforce relationships using primary keys and foreign keys.
- Store customer, account, card, and transaction information.
- Practice SQL queries from basic filtering to multi-table joins and aggregation.
Technologies Used
- Database: MySQL
- Language: SQL
Database Structure
The database is named BankingSystem and contains four tables:
Table	Purpose	Main fields
Customers	Stores customer information and KYC status	CustomerID, CustomerName, Email, Phone, KYCStatus, CreatedDate
Accounts	Stores bank account details and balances	AccountID, CustomerID, AccountNumber, AccountType, Balance, Status, OpenedDate
Cards	Stores card details linked to accounts	CardID, AccountID, CardNumber, CardType, CVV, ExpiryDate
Transactions	Stores account transaction records	TransactionID, AccountID, TransactionType, Amount, TransactionDate, Location, Merchant, DeviceID, Status


Relationships
- Each account references a customer through Accounts.CustomerID.
- Each card references an account through Cards.AccountID.
- Each transaction references an account through Transactions.AccountID.
- Primary keys uniquely identify records; the customer email is also defined as unique.
Features Implemented
- Created the BankingSystem database and four related tables.
- Added sample records: 5 customers, 5 accounts, 5 cards, and 10 transactions.
- Retrieved customer names and email addresses.
- Filtered active accounts and verified customers.
- Found debit transactions above ₹10,000.
- Calculated average account balance and highest transaction amount.
- Counted accounts by account type and customers by KYC status.
- Joined customers with their accounts and card details.
- Counted transactions for each account.
SQL Concepts Demonstrated
- CREATE DATABASE, CREATE TABLE, and INSERT INTO
- PRIMARY KEY, AUTO_INCREMENT, UNIQUE, and FOREIGN KEY
- SELECT, WHERE, and AND
- Aggregate functions: AVG(), MAX(), and COUNT()
- GROUP BY
- INNER JOIN / JOIN
- Column aliases
Setup and Usage
1. Install MySQL Server and open MySQL Workbench or the MySQL command-line client.
2. Run the SQL statements from your project script in order:
   - Create and select the database.
   - Create the four tables.
   - Insert the sample records.
   - Run the example queries.
3. To select the database manually, run:
USE BankingSystem;
If you keep the SQL statements in a file, save it with a .sql extension and execute that file using your preferred MySQL client.
Example Queries
1. Find active accounts
SELECT AccountNumber, Balance, Status
FROM Accounts
WHERE Status = 'Active';
2. Find debit transactions above ₹10,000
SELECT TransactionID, Amount, TransactionType
FROM Transactions
WHERE TransactionType = 'Debit'
  AND Amount > 10000;
3. Show customers and their account balances
SELECT c.CustomerName, a.AccountNumber, a.Balance
FROM Customers AS c
JOIN Accounts AS a
  ON c.CustomerID = a.CustomerID;
4. Count transactions for each account
SELECT a.AccountNumber,
       COUNT(t.TransactionID) AS Total_Transactions
FROM Accounts AS a
JOIN Transactions AS t
  ON a.AccountID = t.AccountID
GROUP BY a.AccountNumber;
Current Scope and Limitations
This is a database design and SQL-query practice project using sample data. The current script demonstrates data storage and reporting queries; it does not implement a banking application interface, authentication, live transfers, automatic fraud detection, or transaction-processing workflows.
The sample data includes card numbers and CVVs for demonstration only. Do not use real payment-card data in this project or publish real card numbers or CVVs. For a production system, sensitive payment data must be handled using appropriate security controls and applicable payment-card standards.
Possible Future Improvements
- Add NOT NULL, CHECK, and other suitable data-integrity constraints.
- Add indexes for frequently queried columns.
- Add queries for monthly transaction summaries and account activity.
- Explore views and stored procedures for reusable reports.
- Add sample queries to flag unusual transaction patterns (as analysis only, not automatic fraud detection).
Learning Outcomes
- Designing related relational tables.
- Defining primary and foreign key constraints.
- Inserting and querying sample records.
- Using filtering, joins, grouping, and aggregate functions.
- Writing SQL reports from a small banking dataset.
