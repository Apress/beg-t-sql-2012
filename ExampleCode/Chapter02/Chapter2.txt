Listing 2-1. Statements Returning Literal Values

SELECT 1
SELECT 'ABC'

Listing 2-2. Writing a Query with a FROM Clause

USE AdventureWorks2012;
GO
SELECT BusinessEntityID, JobTitle
FROM HumanResources.Employee;

Listing 2-3. A Scripted SELECT Statement

SELECT [BusinessEntityID]
,[NationalIDNumber]
,[LoginID]
,[OrganizationNode]
,[OrganizationLevel]
,[JobTitle]
,[BirthDate]
,[MaritalStatus]
,[Gender]
,[HireDate]
,[SalariedFlag]
,[VacationHours]
,[SickLeaveHours]
,[CurrentFlag]
,[rowguid]
,[ModifiedDate]
FROM [AdventureWorks2012].[HumanResources].[Employee]
GO

Listing 2-4. Mixing Literal Values and Column Names

USE AdventureWorks2012;
GO
SELECT 'A Literal Value' AS "Literal Value",
BusinessEntityID AS EmployeeID,
LoginID JobTitle
FROM HumanResources.Employee;

USE AdventureWorks2012;
GO
--1
SELECT CustomerID, SalesOrderID
FROM Sales.SalesOrderHeader
WHERE CustomerID = 11000;
--2
SELECT CustomerID, SalesOrderID
FROM Sales.SalesOrderHeader
WHERE SalesOrderID = 43793;
--3
SELECT CustomerID, SalesOrderID, OrderDate
FROM Sales.SalesOrderHeader
WHERE OrderDate = '2005-07-02';
--4
SELECT BusinessEntityID, LoginID, JobTitle
FROM HumanResources.Employee
WHERE JobTitle = 'Chief Executive Officer';

Listing 2-6. Using Operators with the WHERE Clause

USE AdventureWorks2012;
GO
--Using a DateTime column
--1
SELECT CustomerID, SalesOrderID, OrderDate
FROM Sales.SalesOrderHeader
WHERE OrderDate > '2005-07-05';
--2
SELECT CustomerID, SalesOrderID, OrderDate
FROM Sales.SalesOrderHeader
WHERE OrderDate < '2005-07-05';
--3
SELECT CustomerID, SalesOrderID, OrderDate
FROM Sales.SalesOrderHeader
WHERE OrderDate >= '2005-07-05';
--4
SELECT CustomerID, SalesOrderID, OrderDate
FROM Sales.SalesOrderHeader
WHERE OrderDate <> '2005-07-05';
--5
SELECT CustomerID, SalesOrderID, OrderDate
FROM Sales.SalesOrderHeader
WHERE OrderDate != '2005-07-05';
--Using a numeric column
--6
SELECT SalesOrderID, SalesOrderDetailID, OrderQty
FROM Sales.SalesOrderDetail
WHERE OrderQty > 10;
--7
SELECT SalesOrderID, SalesOrderDetailID, OrderQty
FROM Sales.SalesOrderDetail
WHERE OrderQty <= 10;
--8
SELECT SalesOrderID, SalesOrderDetailID, OrderQty
FROM Sales.SalesOrderDetail
WHERE OrderQty <> 10;
--9
SELECT SalesOrderID, SalesOrderDetailID, OrderQty
FROM Sales.SalesOrderDetail
WHERE OrderQty != 10;
--Using a string column
--10
SELECT BusinessEntityID, FirstName
FROM Person.Person
WHERE FirstName <> 'Catherine';
--11
SELECT BusinessEntityID, FirstName
FROM Person.Person
WHERE FirstName != 'Catherine';
--12
SELECT BusinessEntityID, FirstName
FROM Person.Person
WHERE FirstName > 'M';
--13
SELECT BusinessEntityID, FirstName
FROM Person.Person
WHERE FirstName !> 'M';


USE AdventureWorks2012
GO
--1
SELECT CustomerID, SalesOrderID, OrderDate
FROM Sales.SalesOrderHeader
WHERE OrderDate BETWEEN '2005-07-02' AND '2005-07-04';
--2
SELECT CustomerID, SalesOrderID, OrderDate
FROM Sales.SalesOrderHeader
WHERE CustomerID BETWEEN 25000 AND 25005;
--3
SELECT BusinessEntityID, JobTitle
FROM HumanResources.Employee
WHERE JobTitle BETWEEN 'C' and 'E';
--An invalid BETWEEN expression
--4
SELECT CustomerID, SalesOrderID, OrderDate
FROM Sales.SalesOrderHeader
WHERE CustomerID BETWEEN 25005 AND 25000;


Listing 2-8. Using NOT BETWEEN

Use AdventureWorks2012
GO
--1
SELECT CustomerID, SalesOrderID, OrderDate
FROM Sales.SalesOrderHeader
WHERE OrderDate NOT BETWEEN '2005-07-02' AND '2005-07-04';
--2
SELECT CustomerID, SalesOrderID, OrderDate
FROM Sales.SalesOrderHeader
WHERE CustomerID NOT BETWEEN 25000 AND 25005;
--3
SELECT BusinessEntityID, JobTitle
FROM HumanResources.Employee
WHERE JobTitle NOT BETWEEN 'C' and 'E';
--An invalid BETWEEN expression
--4
SELECT CustomerID, SalesOrderID, OrderDate
FROM Sales.SalesOrderHeader
WHERE CustomerID NOT BETWEEN 25005 AND 25000;


Listing 2-9. Table Setup for Date/Time Example

CREATE TABLE #DateTimeExample(
ID INT NOT NULL IDENTITY PRIMARY KEY,
MyDate DATETIME2(0) NOT NULL,
MyValue VARCHAR(25) NOT NULL
);
GO
INSERT INTO #DateTimeExample
(MyDate,MyValue)
VALUES ('1/2/2009 10:30','Bike'),
('1/3/2009 13:00','Trike'),
('1/3/2009 13:10','Bell'),
('1/3/2009 17:35','Seat');


Listing 2-10. Filtering On Date and Time Columns

--1
SELECT ID, MyDate, MyValue
FROM #DateTimeExample
WHERE MyDate = '2009-01-03';
--2
SELECT ID, MyDate, MyValue
FROM #DateTimeExample
WHERE MyDate BETWEEN '2009-01-03 00:00:00' AND '2009-01-03 23:59:59';


Listing 2-11. Using LIKE with %

USE AdventureWorks2012;
GO
--1
SELECT DISTINCT LastName
FROM Person.Person
WHERE LastName LIKE 'Sand%';
--2
SELECT DISTINCT LastName
FROM Person.Person
WHERE LastName NOT LIKE 'Sand%';
--3
SELECT DISTINCT LastName
FROM Person.Person
WHERE LastName LIKE '%Z%';
--4
SELECT DISTINCT LastName
FROM Person.Person
WHERE LastName LIKE 'Bec_';


Listing 2-12. Using Square Brackets with LIKE

USE AdventureWorks2012;
GO
--1
SELECT DISTINCT LastName
FROM Person.Person
WHERE LastName LIKE 'Cho[i-k]';
--2
SELECT DISTINCT LastName
FROM Person.Person
WHERE LastName LIKE 'Cho[i,j,k]';
--3
SELECT DISTINCT LastName
FROM Person.Person
WHERE LastName LIKE 'Cho[^i]';


Listing 2-13. Combining Wildcards in One Pattern

USE AdventureWorks2012;
GO
--1
SELECT LastName
FROM Person.Person
WHERE LastName LIKE 'Ber[r,g]%';
--2
SELECT LastName
FROM Person.Person
WHERE LastName LIKE 'Ber[^r]%';
--3
SELECT LastName
FROM Person.Person
WHERE LastName LIKE 'Be%n_';

Listing 2-14. How to Use AND and OR

USE AdventureWorks2012;
GO
--1
SELECT BusinessEntityID,FirstName,MiddleName,LastName
FROM Person.Person
WHERE FirstName = 'Ken' AND LastName = 'Myer';
--2
SELECT BusinessEntityID,FirstName,MiddleName,LastName
FROM Person.Person
WHERE LastName = 'Myer' OR LastName = 'Meyer';

Listing 2-15. WHERE Clauses with Three Predicates
USE AdventureWorks2012;
GO
--1
SELECT BusinessEntityID,FirstName,MiddleName,LastName
FROM Person.Person
WHERE FirstName = 'Ken' AND LastName = 'Myer'
OR LastName = 'Meyer';
--2
SELECT BusinessEntityID,FirstName,MiddleName,LastName
FROM Person.Person
WHERE LastName = 'Myer' OR LastName = 'Meyer'
AND FirstName = 'Ken';
--3
SELECT BusinessEntityID,FirstName,MiddleName,LastName
FROM Person.Person
WHERE LastName = 'Meyer'
AND FirstName = 'Ken' OR LastName = 'Myer';
--4
SELECT BusinessEntityID,FirstName,MiddleName,LastName
FROM Person.Person
WHERE FirstName = 'Ken' AND (LastName = 'Myer'
OR LastName = 'Meyer');


Listing 2-16. Using NOT with Parentheses

USE AdventureWorks2012;
GO
--1
SELECT BusinessEntityID,FirstName,MiddleName,LastName
FROM Person.Person
WHERE FirstName='Ken' AND LastName <> 'Myer'
AND LastName <> 'Meyer';
--2
SELECT BusinessEntityID,FirstName,MiddleName,LastName
FROM Person.Person
WHERE FirstName='Ken'
AND NOT (LastName = 'Myer' OR LastName = 'Meyer');

Listing 2-17. Using the IN Operator
USE AdventureWorks2012
GO
--1
SELECT BusinessEntityID,FirstName,MiddleName,LastName
FROM Person.Person
WHERE FirstName = 'Ken' AND
LastName IN ('Myer','Meyer');
--2
SELECT TerritoryID, Name
FROM Sales.SalesTerritory
WHERE TerritoryID IN (2,1,4,5);
--3
SELECT TerritoryID, Name
FROM Sales.SalesTerritory
WHERE TerritoryID NOT IN (2,1,4,5);


Listing 2-18. An Example Illustrating NULL

USE AdventureWorks2012;
GO
--1) Returns 19,972 rows
SELECT MiddleName
FROM Person.Person;
--2) Returns 291 rows
SELECT MiddleName
FROM Person.Person
WHERE MiddleName = 'B';
--3) Returns 11,182 but 19,681 were expected
SELECT MiddleName
FROM Person.Person
WHERE MiddleName != 'B';
--4) Returns 19,681
SELECT MiddleName
FROM Person.Person
WHERE MiddleName IS NULL
OR MiddleName !='B';


Listing 2-19. Using CONTAINS

USE AdventureWorks2012;
GO
--1
SELECT FileName
FROM Production.Document
WHERE Contains(Document,'important');
--2
SELECT FileName
FROM Production.Document
WHERE Contains(Document,' "service guidelines " ')
AND DocumentLevel = 2;'


Listing 2-20. Multiple Terms in CONTAINS

USE AdventureWorks2012;
GO
--1
SELECT FileName, DocumentSummary
FROM Production.Document
WHERE Contains(DocumentSummary,'bicycle AND reflectors');
--2
SELECT FileName, DocumentSummary
FROM Production.Document
WHERE CONTAINS(DocumentSummary,'bicycle AND NOT reflectors');
--3
SELECT FileName, DocumentSummary
FROM Production.Document
WHERE CONTAINS(DocumentSummary,'maintain NEAR bicycle AND NOT reflectors');


USE AdventureWorks2012;
GO
--1
SELECT FileName, DocumentSummary
FROM Production.Document
WHERE CONTAINS((DocumentSummary,Document),'maintain');
--2
SELECT FileName, DocumentSummary
FROM Production.Document
WHERE CONTAINS((DocumentSummary),'maintain')
OR CONTAINS((Document),'maintain')
--3
SELECT FileName, DocumentSummary
FROM Production.Document
WHERE CONTAINS(*,'maintain');


Listing 2-22. Using FREETEXT

USE AdventureWorks2012
GO
--1
SELECT FileName, DocumentSummary
FROM Production.Document
WHERE FREETEXT((DocumentSummary),'provides');
--2
SELECT FileName, DocumentSummary
FROM Production.Document
WHERE DocumentSummary LIKE '%provides%'


Listing 2-23. How to Use ORDER BY

USE AdventureWorks2012;
GO
--1
SELECT ProductID, LocationID
FROM Production.ProductInventory
ORDER BY LocationID;
--2
SELECT ProductID, LocationID
FROM Production.ProductInventory
ORDER BY ProductID, LocationID DESC


Listing 2-24. How to Use ORDER BY OFFSET

SELECT ProductID, LocationID
FROM Production.ProductInventory
ORDER BY LocationID
OFFSET 10 ROWS;


Listing 2-25. How to Use ORDER BY FETCH NEXT…ONLY

SELECT ProductID, LocationID
FROM Production.ProductInventory
ORDER BY LocationID
OFFSET 10 ROWS
FETCH NEXT 10 ROWS ONLY;


Listing 2-26. Learning How to View Execution Plans

USE AdventureWorks2012;
GO
--1
SELECT LastName, FirstName
FROM Person.Person
WHERE LastName = 'Smith';
--2
SELECT LastName, FirstName
FROM Person.Person
WHERE FirstName = 'Ken';
--3
SELECT ModifiedDate
FROM Person.Person
WHERE ModifiedDate BETWEEN '2005-01-01' and '2005-01-31';

