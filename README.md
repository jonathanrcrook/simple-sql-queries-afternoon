# simple-sql-queries

For today we will be practicing inserting and querying data using SQL.

Here is a website that will let us write queries to interact with some data.  [http://jxs.me/chinook-web/](http://jxs.me/chinook-web/)

On the left are the Tables with their fields.  The right is where we will be writing our queries.  The bottom is where we will see our results.  

Any new tables or records that we add into the database will be removed after you refresh the page.  So if you're wondering where you data went, that may be why.

Use [www.sqlteaching.com](http://www.sqlteaching.com/) or [sqlbolt.com](http://sqlbolt.com/) as resources for the missing keywords you'll need.

## PERSON
1. Create a table called Person that records a person's Name, Age, Height, City, FavoriteColor, and Id.  Id should be an auto-incrementing id/primary key.  
2. Add 5 different people into the Person database.  Remember to not include the Id because it should auto-increment.
3. List the people in the Person table by Height from tallest to shortest (descending)


CREATE TABLE person (
	Name text,
  	Age integer,
  	Height text,
  	City text,
  	FavoriteColor text,
  	Id integer primary key autoincrement
);

INSERT INTO person(Name, Age, Height, City, FavoriteColor)
VALUES ('Jon', 30, '5-10', 'Dallas', 'Grey'),
('Ariel', 27, '5-4', 'Dallas', 'Yellow'),
('Toby', 30, '5-9', 'Pheonix', 'Blue'),
('Kurt', 30, '5-11', 'Houston', 'Green'),
('Mike', 22, '5-9', 'LA', 'Red');

SELECT name, height
FROM person
ORDER BY Height DESC;


(For this database to create an auto incrementing field set it's type to INTEGER PRIMARY KEY AUTOINCREMENT)

  * List the people in the Person table by Height from shortest to tallest (ascending)

SELECT name, height
FROM person
ORDER BY Height ASC;

  * List all the people in the Person table by oldest first

SELECT name, age
FROM person
ORDER BY age DESC;

  * List all the people in the Person table older than age 20.

SELECT name, age
FROM person
WHERE age > 20;

  * List all the people in the Person table that are exactly 18.

SELECT name, age
FROM person
WHERE age >= 18;

  * List all Person that are less than 20 and older than 30.

SELECT name, age
FROM person
WHERE age < 20 AND age > 30;

  * List all Person that are not 27 (Use not equals)

SELECT name, age
FROM person
WHERE age != 27;

  * List all Person where their favorite color is not red

SELECT name, favoriteColor
FROM person
WHERE favoriteColor != 'Red';

  * List all Person where their favorite color is not red or blue

SELECT name, favoriteColor
FROM person
WHERE favoriteColor != 'Red' AND favoriteColor != 'Blue';

  * List all Person where their favorite color is orange or green

SELECT name, favoriteColor
FROM person
WHERE favoriteColor IN('Orange', 'Green');


  * List all Person where their favorite color is orange, green or blue (use IN)

SELECT name, favoriteColor
FROM person
WHERE favoriteColor IN('Orange', 'Green', 'Blue');

  * List all Person where their favorite color is yellow or purple

SELECT name, favoriteColor
FROM person
WHERE favoriteColor IN('Yellow', 'Purple');



## ORDER
4. Create a table called Orders that records the productName, productPrice, Quantity, and personId  
5. Add 5 Orders to Order table
6. Select all the records from the Order table

CREATE TABLE orders(
	productName text,
  	productPrice number,
  	quantity number,
  	personId integer primary key autoincrement
);

INSERT INTO orders(productName, productPrice, quantity)
VALUES
('coffee', 3.5, 5),
('apple', .50, 10),
('banana', 1.25, 7),
('eggs', 2.5, 3),
('milk', 2.75, 6)
;

  * Calculate the total number of products Ordered

SELECT SUM(quantity)
FROM orders;


  * Calculate the total Order Price

SELECT SUM(productPrice * quantity)
FROM orders;


  * Calculate the total Order Price By personId (If you only made orders for 1 person, go add more for the other people)

SELECT personid, sum(productprice * quantity) AS order_total
FROM orders
GROUP BY personid;


## Artists
7. Add 3 new Artists to the Artist table

INSERT INTO Artist(Name)
VALUES ('The Wonder Years'),
('Mayday Parade'),
('All Time Low');

 * Select the top 10 artists in reverse alphabetical order

SELECT *
FROM Artist
ORDER BY Name DESC
LIMIT 10;

 * Select the top 5 artists in alphabetical order

SELECT *
FROM Artist
ORDER BY Name ASC
LIMIT 5;

 * Select all artists that start with the word Black

SELECT *
FROM Artist
WHERE Name LIKE "%Black%"

 * Select all artists that contain the word Black

SELECT *
FROM Artist
WHERE Name LIKE "%Black%"

## Employee
8. Add 2 new Employees to the Employee table

INSERT INTO Employee(FirstName, LastName)
VALUES
('Jonathan', 'Crook'),
('Max', 'Rawls');

* List all Employee first and last names only that live in Calgary

SELECT FirstName, LastName, City
FROM Employee
WHERE City = 'Calgary';

* Find the first and last name for the youngest employee

SELECT FirstName, LastName, BirthDate
FROM Employee
ORDER BY BirthDate ASC
LIMIT 1;

* Find the first and last name for the oldest employee

SELECT FirstName, LastName, BirthDate
FROM Employee
ORDER BY BirthDate DESC
LIMIT 1;

* Find everyone that reports to Nancy Edwards (Use the ReportsTo column)

SELECT FirstName, LastName, ReportsTo
FROM Employee
WHERE ReportsTo = 'Nancy Edwards';

* Count how many people live in Lethbridge

SELECT COUNT()
FROM employee
WHERE city = 'Lethbridge';

## Invoice
9. Use the Invoice table for the following

* Count how many orders were made from the USA

SELECT COUNT()
FROM Invoice
WHERE BillingCountry = 'USA';

* Find the largest order total amount

SELECT *
FROM Invoice
ORDER BY Total DESC
LIMIT 1;

* Find the smallest order total amount

SELECT *
FROM Invoice
ORDER BY Total ASC
LIMIT 1;

* Find all orders bigger than $5

SELECT
FROM Invoice
WHERE Total > 5
ORDER BY Total

* Count how many orders were smaller than $5

SELECT COUNT()
FROM Invoice
WHERE Total < 5
ORDER BY Total;

* Count how many orders were in CA, TX, or AZ (use IN)

SELECT COUNT()
FROM Invoice
WHERE BillingState IN ('CA', 'TX', 'AZ');

* Get the average total of the orders

SELECT AVG(Total)
FROM Invoice;

* Get the total sum of the orders

SELECT SUM(Total)
FROM Invoice;


## Copyright

© DevMountain LLC, 2016. Unauthorized use and/or duplication of this material without express and written permission from DevMountain, LLC is strictly prohibited. Excerpts and links may be used, provided that full and clear credit is given to DevMountain with appropriate and specific direction to the original content.
