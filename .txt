CREATE DATABASE BankingSystem;
Query OK, 1 row affected (0.05 sec)

mysql> USE BankingSystem;
Database changed
mysql> CREATE TABLE Customers
    -> (
    ->     CustomerID INT PRIMARY KEY AUTO_INCREMENT,
    ->     CustomerName VARCHAR(100),
    ->     Email VARCHAR(100) UNIQUE,
    ->     Phone VARCHAR(15),
    ->     KYCStatus VARCHAR(20),
    ->     CreatedDate DATETIME
    -> );
Query OK, 0 rows affected (0.10 sec)

mysql> CREATE TABLE Accounts
    -> (
    ->     AccountID INT PRIMARY KEY AUTO_INCREMENT,
    ->     CustomerID INT,
    ->     AccountNumber VARCHAR(20),
    ->     AccountType VARCHAR(20),
    ->     Balance DECIMAL(12,2),
    ->     Status VARCHAR(20),
    ->     OpenedDate DATETIME,
    ->
    ->     FOREIGN KEY(CustomerID)
    ->     REFERENCES Customers(CustomerID)
    -> );
Query OK, 0 rows affected (0.06 sec)

mysql> CREATE TABLE Cards
    -> (
    ->     CardID INT PRIMARY KEY AUTO_INCREMENT,
    ->     AccountID INT,
    ->     CardNumber VARCHAR(20),
    ->     CardType VARCHAR(20),
    ->     CVV INT,
    ->     ExpiryDate DATE,
    ->
    ->     FOREIGN KEY(AccountID)
    ->     REFERENCES Accounts(AccountID)
    -> );
Query OK, 0 rows affected (0.05 sec)

mysql> CREATE TABLE Transactions
    -> (
    ->     TransactionID INT PRIMARY KEY AUTO_INCREMENT,
    ->     AccountID INT,
    ->     TransactionType VARCHAR(20),
    ->     Amount DECIMAL(12,2),
    ->     TransactionDate DATETIME,
    ->     Location VARCHAR(50),
    ->     Merchant VARCHAR(100),
    ->     DeviceID VARCHAR(30),
    ->     Status VARCHAR(20),
    ->
    ->     FOREIGN KEY(AccountID)
    ->     REFERENCES Accounts(AccountID)
    -> );
Query OK, 0 rows affected (0.06 sec)

mysql> INSERT INTO Customers
    -> (CustomerName,Email,Phone,KYCStatus,CreatedDate)
    ->
    -> VALUES
    ->
    -> ('Rahul Kumar','rahul@gmail.com','9876543210','Verified','2025-07-01'),
    ->
    -> ('Priya Sharma','priya@gmail.com','9876543211','Verified','2025-07-01'),
    ->
    -> ('Kiran Reddy','kiran@gmail.com','9876543212','Verified','2025-07-01'),
    ->
    -> ('Sneha Rao','sneha@gmail.com','9876543213','Pending','2025-07-02'),
    ->
    -> ('Arjun Singh','arjun@gmail.com','9876543214','Verified','2025-07-02');
Query OK, 5 rows affected (0.03 sec)
Records: 5  Duplicates: 0  Warnings: 0

mysql> INSERT INTO Accounts
    -> (CustomerID,AccountNumber,AccountType,Balance,Status,OpenedDate)
    ->
    -> VALUES
    ->
    -> (1,'ACC1001','Savings',90000,'Active','2025-07-01'),
    ->
    -> (2,'ACC1002','Current',50000,'Active','2025-07-01'),
    ->
    -> (3,'ACC1003','Savings',70000,'Active','2025-07-02'),
    ->
    -> (4,'ACC1004','Savings',100000,'Active','2025-07-02'),
    ->
    -> (5,'ACC1005','Current',40000,'Frozen','2025-07-03');
Query OK, 5 rows affected (0.02 sec)
Records: 5  Duplicates: 0  Warnings: 0

mysql> INSERT INTO Cards
    -> (AccountID,CardNumber,CardType,CVV,ExpiryDate)
    ->
    -> VALUES
    ->
    -> (1,'1111222233334444','Debit',321,'2028-12-31'),
    ->
    -> (2,'5555666677778888','Credit',456,'2027-10-31'),
    ->
    -> (3,'9999000011112222','Debit',654,'2029-08-31'),
    ->
    -> (4,'3333444455556666','Credit',789,'2027-06-30'),
    ->
    -> (5,'7777888899990000','Debit',852,'2028-09-30');
Query OK, 5 rows affected (0.01 sec)
Records: 5  Duplicates: 0  Warnings: 0

mysql> INSERT INTO Transactions
    -> (AccountID,TransactionType,Amount,TransactionDate,Location,Merchant,DeviceID,Status)
    ->
    -> VALUES
    ->
    -> (1,'Debit',2000,'2025-07-10 09:00:00','Hyderabad','Amazon','DEV001','Success'),
    ->
    -> (1,'Debit',50000,'2025-07-10 09:05:00','Delhi','Flipkart','DEV002','Success'),
    ->
    -> (1,'Debit',60000,'2025-07-10 09:08:00','Mumbai','Zomato','DEV003','Success'),
    ->
    -> (2,'Credit',10000,'2025-07-11 10:00:00','Chennai','Salary','DEV004','Success'),
    ->
    -> (2,'Debit',80000,'2025-07-11 10:05:00','Chennai','Jewellery','DEV005','Success'),
    ->
    -> (3,'Debit',15000,'2025-07-12 09:00:00','Vizag','Swiggy','DEV006','Success'),
    ->
    -> (3,'Credit',25000,'2025-07-12 10:30:00','Vizag','Cash Deposit','DEV006','Success'),
    ->
    -> (4,'Debit',1000,'2025-07-13 09:30:00','Bangalore','BookMyShow','DEV007','Failed'),
    ->
    -> (4,'Debit',70000,'2025-07-13 09:45:00','Mumbai','Luxury Store','DEV008','Success'),
    ->
    -> (5,'Credit',5000,'2025-07-14 08:00:00','Delhi','Salary','DEV009','Success');
Query OK, 10 rows affected (0.01 sec)
Records: 10  Duplicates: 0  Warnings: 0

mysql> SELECT * FROM Customers;
+------------+--------------+-----------------+------------+-----------+---------------------+
| CustomerID | CustomerName | Email           | Phone      | KYCStatus | CreatedDate         |
+------------+--------------+-----------------+------------+-----------+---------------------+
|          1 | Rahul Kumar  | rahul@gmail.com | 9876543210 | Verified  | 2025-07-01 00:00:00 |
|          2 | Priya Sharma | priya@gmail.com | 9876543211 | Verified  | 2025-07-01 00:00:00 |
|          3 | Kiran Reddy  | kiran@gmail.com | 9876543212 | Verified  | 2025-07-01 00:00:00 |
|          4 | Sneha Rao    | sneha@gmail.com | 9876543213 | Pending   | 2025-07-02 00:00:00 |
|          5 | Arjun Singh  | arjun@gmail.com | 9876543214 | Verified  | 2025-07-02 00:00:00 |
+------------+--------------+-----------------+------------+-----------+---------------------+
5 rows in set (0.01 sec)

mysql>
mysql> SELECT * FROM Accounts;
+-----------+------------+---------------+-------------+-----------+--------+---------------------+
| AccountID | CustomerID | AccountNumber | AccountType | Balance   | Status | OpenedDate          |
+-----------+------------+---------------+-------------+-----------+--------+---------------------+
|         1 |          1 | ACC1001       | Savings     |  90000.00 | Active | 2025-07-01 00:00:00 |
|         2 |          2 | ACC1002       | Current     |  50000.00 | Active | 2025-07-01 00:00:00 |
|         3 |          3 | ACC1003       | Savings     |  70000.00 | Active | 2025-07-02 00:00:00 |
|         4 |          4 | ACC1004       | Savings     | 100000.00 | Active | 2025-07-02 00:00:00 |
|         5 |          5 | ACC1005       | Current     |  40000.00 | Frozen | 2025-07-03 00:00:00 |
+-----------+------------+---------------+-------------+-----------+--------+---------------------+
5 rows in set (0.00 sec)

mysql>
mysql> SELECT * FROM Cards;
+--------+-----------+------------------+----------+------+------------+
| CardID | AccountID | CardNumber       | CardType | CVV  | ExpiryDate |
+--------+-----------+------------------+----------+------+------------+
|      1 |         1 | 1111222233334444 | Debit    |  321 | 2028-12-31 |
|      2 |         2 | 5555666677778888 | Credit   |  456 | 2027-10-31 |
|      3 |         3 | 9999000011112222 | Debit    |  654 | 2029-08-31 |
|      4 |         4 | 3333444455556666 | Credit   |  789 | 2027-06-30 |
|      5 |         5 | 7777888899990000 | Debit    |  852 | 2028-09-30 |
+--------+-----------+------------------+----------+------+------------+
5 rows in set (0.00 sec)

mysql>
mysql> SELECT * FROM Transactions;
+---------------+-----------+-----------------+----------+---------------------+-----------+--------------+----------+---------+
| TransactionID | AccountID | TransactionType | Amount   | TransactionDate     | Location  | Merchant     | DeviceID | Status  |
+---------------+-----------+-----------------+----------+---------------------+-----------+--------------+----------+---------+
|             1 |         1 | Debit           |  2000.00 | 2025-07-10 09:00:00 | Hyderabad | Amazon       | DEV001   | Success |
|             2 |         1 | Debit           | 50000.00 | 2025-07-10 09:05:00 | Delhi     | Flipkart     | DEV002   | Success |
|             3 |         1 | Debit           | 60000.00 | 2025-07-10 09:08:00 | Mumbai    | Zomato       | DEV003   | Success |
|             4 |         2 | Credit          | 10000.00 | 2025-07-11 10:00:00 | Chennai   | Salary       | DEV004   | Success |
|             5 |         2 | Debit           | 80000.00 | 2025-07-11 10:05:00 | Chennai   | Jewellery    | DEV005   | Success |
|             6 |         3 | Debit           | 15000.00 | 2025-07-12 09:00:00 | Vizag     | Swiggy       | DEV006   | Success |
|             7 |         3 | Credit          | 25000.00 | 2025-07-12 10:30:00 | Vizag     | Cash Deposit | DEV006   | Success |
|             8 |         4 | Debit           |  1000.00 | 2025-07-13 09:30:00 | Bangalore | BookMyShow   | DEV007   | Failed  |
|             9 |         4 | Debit           | 70000.00 | 2025-07-13 09:45:00 | Mumbai    | Luxury Store | DEV008   | Success |
|            10 |         5 | Credit          |  5000.00 | 2025-07-14 08:00:00 | Delhi     | Salary       | DEV009   | Success |
+---------------+-----------+-----------------+----------+---------------------+-----------+--------------+----------+---------+
10 rows in set (0.00 sec)

mysql>mysql> -- EASY QUERIES
mysql>
mysql> -- 1. Returns all customer names and email addresses.
mysql> SELECT CustomerName, Email
    -> FROM Customers;
+--------------+-----------------+
| CustomerName | Email           |
+--------------+-----------------+
| Rahul Kumar  | rahul@gmail.com |
| Priya Sharma | priya@gmail.com |
| Kiran Reddy  | kiran@gmail.com |
| Sneha Rao    | sneha@gmail.com |
| Arjun Singh  | arjun@gmail.com |
+--------------+-----------------+
5 rows in set (0.00 sec)

mysql>
mysql> -- 2. Returns all active bank accounts using WHERE clause.
mysql> SELECT AccountNumber, Balance, Status
    -> FROM Accounts
    -> WHERE Status = 'Active';
+---------------+-----------+--------+
| AccountNumber | Balance   | Status |
+---------------+-----------+--------+
| ACC1001       |  90000.00 | Active |
| ACC1002       |  50000.00 | Active |
| ACC1003       |  70000.00 | Active |
| ACC1004       | 100000.00 | Active |
+---------------+-----------+--------+
4 rows in set (0.00 sec)

mysql>
mysql> -- 3. Returns all debit transactions greater than ₹10000 using WHERE clause.
mysql> SELECT TransactionID, Amount, TransactionType
    -> FROM Transactions
    -> WHERE TransactionType = 'Debit'
    -> AND Amount > 10000;
+---------------+----------+-----------------+
| TransactionID | Amount   | TransactionType |
+---------------+----------+-----------------+
|             2 | 50000.00 | Debit           |
|             3 | 60000.00 | Debit           |
|             5 | 80000.00 | Debit           |
|             6 | 15000.00 | Debit           |
|             9 | 70000.00 | Debit           |
+---------------+----------+-----------------+
5 rows in set (0.00 sec)

mysql>
mysql> -- 4. Returns customers whose KYC status is Verified using WHERE clause.
mysql> SELECT CustomerName, KYCStatus
    -> FROM Customers
    -> WHERE KYCStatus = 'Verified';
+--------------+-----------+
| CustomerName | KYCStatus |
+--------------+-----------+
| Rahul Kumar  | Verified  |
| Priya Sharma | Verified  |
| Kiran Reddy  | Verified  |
| Arjun Singh  | Verified  |
+--------------+-----------+
4 rows in set (0.00 sec)

mysql>
mysql>
mysql>
mysql> -- MEDIUM LEVEL QUERIES
mysql>
mysql> -- 1. Returns average account balance using AVG aggregate function.
mysql> SELECT AVG(Balance) AS Average_Balance
    -> FROM Accounts;
+-----------------+
| Average_Balance |
+-----------------+
|    70000.000000 |
+-----------------+
1 row in set (0.00 sec)

mysql>
mysql> -- 2. Returns total number of accounts based on account type using COUNT and GROUP BY clauses.
mysql> SELECT AccountType,
    -> COUNT(AccountID) AS Total_Accounts
    -> FROM Accounts
    -> GROUP BY AccountType;
+-------------+----------------+
| AccountType | Total_Accounts |
+-------------+----------------+
| Savings     |              3 |
| Current     |              2 |
+-------------+----------------+
2 rows in set (0.00 sec)

mysql>
mysql> -- 3. Returns highest transaction amount using MAX aggregate function.
mysql> SELECT MAX(Amount) AS Highest_Transaction
    -> FROM Transactions;
+---------------------+
| Highest_Transaction |
+---------------------+
|            80000.00 |
+---------------------+
1 row in set (0.00 sec)

mysql>
mysql> -- 4. Returns total customers based on KYC status using COUNT and GROUP BY clauses.
mysql> SELECT KYCStatus,
    -> COUNT(CustomerID) AS Total_Customers
    -> FROM Customers
    -> GROUP BY KYCStatus;
+-----------+-----------------+
| KYCStatus | Total_Customers |
+-----------+-----------------+
| Verified  |               4 |
| Pending   |               1 |
+-----------+-----------------+
2 rows in set (0.00 sec)

mysql>
mysql>
mysql>
mysql> -- HARD LEVEL QUERIES
mysql>
mysql> -- 1. Returns customer names along with account numbers and balances using JOIN clause.
mysql> SELECT
    -> c.CustomerName,
    -> a.AccountNumber,
    -> a.Balance
    -> FROM Customers c
    -> JOIN Accounts a
    -> ON c.CustomerID = a.CustomerID;
+--------------+---------------+-----------+
| CustomerName | AccountNumber | Balance   |
+--------------+---------------+-----------+
| Rahul Kumar  | ACC1001       |  90000.00 |
| Priya Sharma | ACC1002       |  50000.00 |
| Kiran Reddy  | ACC1003       |  70000.00 |
| Sneha Rao    | ACC1004       | 100000.00 |
| Arjun Singh  | ACC1005       |  40000.00 |
+--------------+---------------+-----------+
5 rows in set (0.00 sec)

mysql>
mysql> -- 2. Returns customer names along with card type using JOIN clause.
mysql> SELECT
    -> c.CustomerName,
    -> ca.CardType
    -> FROM Customers c
    -> JOIN Accounts a
    -> ON c.CustomerID = a.CustomerID
    -> JOIN Cards ca
    -> ON a.AccountID = ca.AccountID;
+--------------+----------+
| CustomerName | CardType |
+--------------+----------+
| Rahul Kumar  | Debit    |
| Priya Sharma | Credit   |
| Kiran Reddy  | Debit    |
| Sneha Rao    | Credit   |
| Arjun Singh  | Debit    |
+--------------+----------+
5 rows in set (0.00 sec)

mysql>
mysql> -- 3. Returns customers whose account balance is greater than ₹80000 using JOIN and WHERE clauses.
mysql> SELECT
    -> c.CustomerName,
    -> a.Balance
    -> FROM Customers c
    -> JOIN Accounts a
    -> ON c.CustomerID = a.CustomerID
    -> WHERE a.Balance > 80000;
+--------------+-----------+
| CustomerName | Balance   |
+--------------+-----------+
| Rahul Kumar  |  90000.00 |
| Sneha Rao    | 100000.00 |
+--------------+-----------+
2 rows in set (0.00 sec)

mysql>
mysql> -- 4. Returns total number of transactions performed by each account using JOIN, COUNT and GROUP BY clauses.
mysql> SELECT
    -> a.AccountNumber,
    -> COUNT(t.TransactionID) AS Total_Transactions
    -> FROM Accounts a
    -> JOIN Transactions t
    -> ON a.AccountID = t.AccountID
    -> GROUP BY a.AccountNumber;
+---------------+--------------------+
| AccountNumber | Total_Transactions |
+---------------+--------------------+
| ACC1001       |                  3 |
| ACC1002       |                  2 |
| ACC1003       |                  2 |
| ACC1004       |                  2 |
| ACC1005       |                  1 |
+---------------+--------------------+
5 rows in set (0.00 sec)

mysql>
mysql>
mysql>
mysql> -- :::::::::::::::::::::::::::::::::::::::::::::DESCRIPTION OF QUERIES::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::
mysql>
mysql>
mysql> -- EASY QUERY 1:
mysql> -- This query displays the names and email addresses of all customers using the SELECT statement.
mysql>
mysql> -- EASY QUERY 2:
mysql> -- This query displays the account number, balance, and status of all active bank accounts using the WHERE clause.
mysql>
mysql> -- EASY QUERY 3:
mysql> -- This query returns all debit transactions whose amount is greater than ₹10000 using the WHERE clause with multiple conditions.
mysql>
mysql> -- EASY QUERY 4:
mysql> -- This query displays the names of customers whose KYC verification status is Verified using the WHERE clause.
mysql>
mysql> -- INTERMEDIATE QUERY 1:
mysql> -- This query calculates the average account balance of all bank accounts using the AVG aggregate function.
mysql>
mysql> -- INTERMEDIATE QUERY 2:
mysql> -- This query counts the total number of accounts for each account type using the COUNT aggregate function and GROUP BY clause.
mysql>
mysql> -- INTERMEDIATE QUERY 3:
mysql> -- This query finds the highest transaction amount recorded in the Transactions table using the MAX aggregate function.
mysql>
mysql> -- INTERMEDIATE QUERY 4:
mysql> -- This query counts the total number of customers based on their KYC verification status using COUNT and GROUP BY clauses.
mysql>
mysql> -- HARD QUERY 1:
mysql> -- This query joins the Customers and Accounts tables to display customer names along with their account numbers and balances using the JOIN clause.
mysql>
mysql> -- HARD QUERY 2:
mysql> -- This query joins the Customers, Accounts, and Cards tables to display customer names along with their card types using the JOIN clause.
mysql>
mysql> -- HARD QUERY 3:
mysql> -- This query joins the Customers and Accounts tables and displays customers whose account balance is greater than ₹80000 using JOIN and WHERE clauses.
mysql>
mysql> -- HARD QUERY 4:
mysql> -- This query joins the Accounts and Transactions tables and counts the total number of transactions performed by each account using JOIN, COUNT, and GROUP BY clauses.
mysql>EXIT
