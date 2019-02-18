# Database Queries

## find all customers that live in London. Returns 6 records.
SELECT CustomerName FROM [Customers] where city = 'London'

## CustomerName
Around the Horn
B's Beverages
Consolidated Holdings
Eastern Connection
North/South
Seven Seas Imports




## find all customers with postal code 1010. Returns 3 customers.

SELECT CustomerName FROM [Customers] where PostalCode = 1010

## CustomerName
Cactus Comidas para llevar
Océano Atlántico Ltda.
Rancho grande



## find the phone number for the supplier with the id 11. Should be (010) 9984510.

SELECT Phone FROM [Suppliers] where SupplierID = 11

Phone
(010) 9984510

## list orders descending by the order date. The order with date 1997-02-12 should be at the top.

SELECT * FROM [Orders] order by OrderDate desc

Number of Records: 196
OrderID	CustomerID	EmployeeID	OrderDate	ShipperID
10443	66	8	1997-02-12	1
10442	20	3	1997-02-11	2
10440	71	4	1997-02-10	2
10441	55	3	1997-02-10	2
10439	51	6	1997-02-07	3


## find all suppliers who have names longer than 20 characters. You can use `length(SupplierName)` to get the length of the name. Returns 11 records.
SELECT SupplierName FROM [Suppliers] where length(SupplierName) > 20

Number of Records: 11
SupplierName
New Orleans Cajun Delights
Grandma Kelly's Homestead
Cooperativa de Quesos 'Las Cabras'
Specialty Biscuits, Ltd.
Refrescos Americanas LTDA
Heli Süßwaren GmbH & Co. KG
Plutzer Lebensmittelgroßmärkte AG
Nord-Ost-Fisch Handelsgesellschaft mbH
Formaggi Fortini s.r.l.
Aux joyeux ecclésiastiques
New England Seafood Cannery


## find all customers that include the word "market" in the name. Should return 4 records.

SELECT CustomerName FROM [Customers] where CustomerName like '%market%'

Number of Records: 4
CustomerName
Bottom-Dollar Marketse
Great Lakes Food Market
Save-a-lot Markets
White Clover Markets

## add a customer record for _"The Shire"_, the contact name is _"Bilbo Baggins"_ the address is _"1 Hobbit-Hole"_ in _"Bag End"_, postal code _"111"_ and the country is _"Middle Earth"_.

INSERT INTO Customers (CustomerName, ContactName, Address, City, PostalCode, Country)
VALUES ('The Shire', 'Bilbo Baggins', '1 Hobbit-Hole', 'Bag End', '111', 'Middle Earth');

CustomerID	CustomerName	ContactName	Address	City	PostalCode	Country
92	The Shire	Bilbo Baggins	1 Hobbit-Hole	Bag End	111	Middle Earth

## update _Bilbo Baggins_ record so that the postal code changes to _"11122"_.

UPDATE Customers
SET PostalCode = 11122
WHERE ContactName = 'Bilbo Baggins';

92	The Shire	Bilbo Baggins	1 Hobbit-Hole	Bag End	11122	Middle Earth


## list orders grouped by customer showing the number of orders per customer. _Rattlesnake Canyon Grocery_ should have 7 orders.

SELECT Orders.CustomerId, Customers.CustomerName, Count(OrderID)
FROM Orders
INNER JOIN Customers
ON Orders.CustomerID=Customers.CustomerID
Group by CustomerName 

Number of Records: 74
CustomerID	CustomerName	Count(OrderID)
2	Ana Trujillo Emparedados y helados	1
3	Antonio Moreno Taquería	1
4	Around the Horn	2
11	B's Beverages	1
5	Berglunds snabbköp	3



## list customers names and the number of orders per customer. Sort the list by number of orders in descending order. _Ernst Handel_ should be at the top with 10 orders followed by _QUICK-Stop_, _Rattlesnake Canyon Grocery_ and _Wartian Herkku_ with 7 orders each.

## list orders grouped by customer's city showing number of orders per city. Returns 58 Records with _Aachen_ showing 2 orders and _Albuquerque_ showing 7 orders.

## delete all users that have no orders. Should delete 17 (or 18 if you haven't deleted the record added) records.


From sqlite studio:

PRAGMA foreign_keys = 0;

CREATE TABLE sqlitestudio_temp_table AS SELECT *
                                          FROM accounts;

DROP TABLE accounts;

CREATE TABLE accounts (
    id     INTEGER       PRIMARY KEY AUTOINCREMENT
                         NOT NULL
                         UNIQUE,
    name   VARCHAR (255) UNIQUE
                         NOT NULL,
    budget DECIMAL       NOT NULL
);

INSERT INTO accounts (
                         id,
                         name
                     )
                     SELECT id,
                            name
                       FROM sqlitestudio_temp_table;

DROP TABLE sqlitestudio_temp_table;

PRAGMA foreign_keys = 1;
