# SQL_Feb23
NZSSN SQL training - February 2023

**I'm currently attending th NZSSN Feb '23 course taught by Daniel Fryer** 👩‍🎓
__Fun but challenging so far 😥
Here's a copy of some of my coding exercises. Enjoy__ 😁

-- __Exercise 2.7.1__ --

-- 1. Retrieve only the names of all pets.

-- I try to see all the columns first to know which have the names

`Select *
From Notes.Pets
`
-- Columns are petID, petname, petDOB, FriendID

`Select PetName
From Notes.Pets
`

--2. Retrieve the names of all pets that belong to the friend with FriendID
--equal to 3. Do not join any tables

`Select PetName
From Notes.Pets 
Where FriendID = 3
`

--3. Display the first and last names of all friends whose favourite colour is red.

`Select *
From Notes.Friends
`

-- Columns are FriendID, firstname, lastname, favcolor (I didn't pay attendtion to upper or lower case)


`Select FirstName, lastname
From Notes.Friends
Where FavColour = 'red';
`

-- First attempt it gave only lastname column because I missed out the comma after firstname

--4. Execute the following query and explain what it does
  
`SELECT ScratcherID, ScratchDate, ScratchTime, ScratcheeID
FROM Notes.Scratched -- in MySQL, use Notes_Scratched instead
WHERE ScratchDate = '20180905'
`

-- The query is to filter the rows and scratcherID, scratchdate, scratchTime and ScratcheeID columns  
-- from the notes.scratched table, for the scratch date '2018-09-05'

-- 5. Return all records where ScratchDate is on or before 6th Sep, 2018

`SELECT ScratcherID, ScratchDate, ScratchTime, ScratcheeID
FROM Notes.Scratched 
WHERE ScratchDate <= '20180906'
`

-- 6. Retrieve the ScratcheeID and ScratcherID for all people who have
-- participated in back scratching between the hours of 11AM and 12PM (inclusive).

`SELECT ScratcheeID, ScratcherID
FROM Notes.Scratched 
WHERE ScratchTime >='11:00:00' AND ScratchTime <= '12:00:00';
`

-- Recurrent errors at first because I forgot to include the attribute (column) name after AND 

-- 7. Retrieve the ScratcherID for all people who scratched a back either
-- at 11AM on Sep 6th, 2018, or at 10AM on Sep 7th, 2018

`Select ScratcherID
From Notes.Scratched
Where ScratchDate = '20180906' AND ScratchTime = '11:00:00' 
    OR ScratchDate = '20180907' AND ScratchTime = '10:00:00'
`

-- __Exercise 2.7.2__ --

-- 1. Retrieve the Colours table, but rename the Comments column to ‘Ape Opinions’.

`
Select *
From Ape.Colours;`  -- To view the columns on the table

`
SELECT Comments AS 'Ape Opinions'
From Ape.Colours;
`

-- 2. Order the Colours table, in descending order of colour names 

`
SELECT *
FROM Ape.Colours
ORDER BY ColourName DESC;
`


-- 3. Order the Scratched table by date of scratching and time of scratching

`
SELECT *
FROM Notes.Scratched
ORDER BY ScratchDate, ScratchTime;
`

-- 4. Order the Scratched table by date of scratching (desc) and time of scratching (asc)

`
SELECT *
FROM Notes.Scratched
ORDER BY ScratchDate DESC, ScratchTime ASC;
`
-- Seems ASC order is the default so even if not specified after ScratchTime, will still be in ascending order


-- 5. Reproduce the Colours table, but rename the colour ‘magenta’ to purple, and the colour ‘turquoise’ to ‘blue’ p.68 

`
SELECT ColourID, ColourName, Comments,
        CASE WHEN ColourName = 'magenta' THEN 'purple'
             WHEN ColourName = 'turquoise' THEN 'blue' 
        ELSE ColourName END AS SimplerColourNames
FROM Ape.Colours
`

-- 'Case when' creates a new column, better to name it in the query. It doesn't replace the values in the existing Colour column
-- Kept having errors because no comma after the last specified column name before 'case when'


--__Exercise 2.7.3__ --

-- 1. Use the IN operator to return the names of all home owners in the postcodes 3128, 3142 and 3083

`
Select *
FROM Notes.Houses
`
-- To view table

`
SELECT house_owner, post_code
FROM Notes.Houses
WHERE post_code IN (3128, 3142, 3083) 
`

-- alternative query below  --

`
SELECT house_owner, post_code
FROM Notes.Houses
WHERE post_code = '3128' OR post_code = '3142' OR post_code = '3083' 
`

-- 2. Use the LIKE operator to get the street address (ignoring suburb name) of all houses that are on an avenue.

`
SELECT house_address 
FROM Notes.Houses 
WHERE house_address LIKE '%Ave' 
`

-- 3. Use NOT, with LIKE, to get the house_ID of every house that is not on an avenue.

`
SELECT house_ID, house_address 
FROM Notes.Houses 
WHERE house_address NOT LIKE '%Ave' 
`

--- 4. Houses with post code starting with ‘31’ and that also cost strictly less than $300,000.

`
SELECT house_address, post_code, house_price
FROM Notes.Houses
WHERE post_code LIKE '31%' AND house_price < 300000;
`

-- alternatively --

`
SELECT house_address, post_code, house_price
FROM Notes.Houses
WHERE post_code LIKE '31__' AND house_price < 300000;
`

`
SELECT house_address, post_code, house_price
FROM Notes.Houses
WHERE post_code LIKE '31__%' AND house_price < 300000;
`

-- 'IN' and comparison operator '=' did not work for postcodes using wildcard symbol, only when full postcode specified
-- After 'IN' round brackets must be used, else error. 

`
SELECT house_address, post_code, house_price
FROM Notes.Houses
WHERE post_code = 3128 AND house_price < 300000;
`

`
SELECT house_address, post_code, house_price
FROM Notes.Houses
WHERE post_code IN (3128) AND house_price < 300000;
`

-- 5. Use BETWEEN to find all suburbs with a 40%–70% vaccination rate.

`
SELECT suburb_name, vaccination_rate
FROM Notes.Suburbs
WHERE vaccination_rate BETWEEN 0.40 AND 0.70;
`

-- Instead of

`
SELECT suburb_name, vaccination_rate
FROM Notes.Suburbs
WHERE vaccination_rate >= 0.40 AND vaccination_rate <= 0.70;
`

-- __Exercise 2.7.4__ --

-- 1. 

`
SELECT *
FROM Notes.Friends 
WHERE FavColour = NULL;
`

-- It returns no values because it is looking for any colour = NULL (the true statement), meanwhile
-- any colour = NULL is NULL, not true
-- Instead use query,

`
SELECT *
FROM Notes.Friends 
WHERE FavColour IS NULL;
`


-- 2. Use the IS NULL operator to find all houses where the post code is unknown.

`
SELECT house_ID, house_address
FROM Notes.Houses
WHERE post_code IS NULL  
`


-- 3. Find all houses where the post_code is not unknown.

`
SELECT house_ID, house_address
FROM Notes.Houses
WHERE post_code IS NOT NULL 
`


-- 4. Retrieve all house IDs and postcodes from the Houses table, but for any NULL postcodes, change the entry to ‘UNKNOWN’. 
-- The postcode column in the result table should be called ‘post_code_modified’.


`
SELECT house_ID, post_code,
    CASE WHEN post_code IS NULL THEN 'UNKNOWN' 
    ELSE post_code END AS 'post_code_modified'
FROM Notes.Houses
`

-- used ' = NULL - at first and the NULLs still were NULLs in the new column 



-- __Exercise 2.7.5__ --

--1. From the joined table, how many pets does the friend named ‘Z’ have, and what are their names?

`
SELECT *
FROM Notes.Pets 
`

`
SELECT *
FROM Notes.Friends
`

`
SELECT *
FROM Notes.Friends F JOIN Notes.Pets P ON F.FriendID = P.FriendID
`

-- The joined table specific result for 'Z' 

`
SELECT FirstName, PetName
FROM Notes.Friends F JOIN Notes.Pets P ON F.FriendID = P.FriendID
WHERE FirstName = 'Z'
`


--2. 

-- To view both tables to determine the right PK and FK --

`
SELECT *
FROM Notes.Table1 
`

`
SELECT *
FROM Notes.Table2
`

-- Join on columns A

`
SELECT B, C, D 
FROM Notes.Table1 T1 JOIN Notes.Table2 T2 ON T1.A = T2.A;
`

-- Textbook solution specified cols as T1.B, T1.C, T2.D --

--For fun --

`
SELECT CONCAT(B, C, D) AS WiseQuotes
FROM Notes.Table1 T1 JOIN Notes.Table2 T2 ON T1.A = T2.A;
`


-- 3. 

`
SELECT *
FROM Ape.Friends; 
`

`
SELECT *
FROM Ape.Colours; 
 `
 
 -- To view the tables. PK - ColourID on Ape.Colours table, FK - FavColourID on Ape.Friends table

`
SELECT FirstName, LastName, 
       SUBSTRING (FirstName, 1, 1) AS FirstInitial,
       SUBSTRING (LastName, 1, 1) AS LastInitial
FROM Ape.Friends;
`

-- To check that the initials correspond using the query 


-- for all apes that have a favourite colour, list their initials, next to the name of their favourite colour
-- So Ape.Friends and Ape.Colours tables must be joined 

`
SELECT ColourName,
       SUBSTRING (FirstName, 1, 1) AS FirstInitial,
       SUBSTRING (LastName, 1, 1) AS LastInitial
FROM Ape.Colours AC JOIN Ape.Friends AF ON AC.ColourID = AF.FavColourID
`

-- I added col names FirstInitial, LastInitial, after SELECT and it ran errors as those cols hadn't been created yet


-- 4. Include any apes that do not have a favourite colour

-- The entry with NULL is on Ape.Friends and AF table is on the Right of the query, so use RIGHT JOIN 

`
SELECT ColourName,
       SUBSTRING (FirstName, 1, 1) AS FirstInitial,
       SUBSTRING (LastName, 1, 1) AS LastInitial
FROM Ape.Colours AC RIGHT JOIN Ape.Friends AF ON AC.ColourID = AF.FavColourID
`


-- 5. Include any colours that are not the favourite of any ape


`
SELECT ColourName,
       SUBSTRING (FirstName, 1, 1) AS FirstInitial,
       SUBSTRING (LastName, 1, 1) AS LastInitial
FROM Ape.Colours AC LEFT JOIN Ape.Friends AF ON AC.ColourID = AF.FavColourID
`

-- __Exercise 2.7.6__ --

-- Sample join query for joining 3 tables --

`
SELECT *
FROM Table1 T1
JOIN Table2 T2 ON T1.attribute1 = T2.attribute2
JOIN Table3 T3 ON T2.attribute3 = T3.attribute4;
`

-- 1. Join the EatingFrom table to both the BananaTree table and the Friends table

`
SELECT *
FROM Ape.EatingFrom
`

-- Ape.EatingFrom has no PK, both cols - FriendID and TreeID - have repetitions. 

`
SELECT *
FROM Ape.BananaTree
`

-- Ape.BananaTree has a PK. TreeID col has no repetitions 

`
SELECT *
FROM Ape.Friends;
`

-- Notes.Friends has a PK. FriendID col has no repetitions

-- Due to having common keys to other tables, EatingFrom will be in the middle (T2). BananaTree will be T1 and Friends, T3.--


`
SELECT *
FROM Ape.BananaTree T1
    JOIN Ape.EatingFrom T2 ON T1.TreeID = T2.TreeID
    JOIN Ape.Friends T3 ON T2.FriendID = T3.FriendID;
`


-- 2. Only produce results for trees planted in July 2016


`
SELECT T1.TreeID, T1.MonthPlanted, T1.YearPlanted
FROM Ape.BananaTree T1
    JOIN Ape.EatingFrom T2 ON T1.TreeID = T2.TreeID
    JOIN Ape.Friends T3 ON T2.FriendID = T3.FriendID
WHERE YearPlanted = '2016' AND MonthPlanted = '7'
`


-- 3. 

`
SELECT *
FROM Notes.Scratched
`

-- Table has no PK. ScratcherID and ScratcheeID both have repeated nos from 1 - 3

`
SELECT *
FROM Notes.Friends
`

-- Table has PK - FriendID, nos 1 - 3


-- Join Friends to Scratched


-- For scratchers

`
SELECT FirstName, ScratcherID, ScratchDate, ScratchTime
FROM Notes.Friends T1 JOIN Notes.Scratched T2 ON T1.FriendID = T2.ScratcherID   
`

`
SELECT FirstName AS 'ScratcherName', ScratcherID, ScratchDate, ScratchTime
FROM Notes.Friends T1 JOIN Notes.Scratched T2 ON T1.FriendID = T2.ScratcherID  
ORDER BY ScratchDate ASC
`

-- -- For scratchees

`
SELECT FirstName AS 'ScratcheeName', ScratcheeID, ScratchDate, ScratchTime
FROM Notes.Friends T1 JOIN Notes.Scratched T2 ON T1.FriendID = T2.ScratcheeID  
ORDER BY ScratchDate ASC
`

-- give diff tables, in different order dep on join cols
-- tried joining Notes.Friends twice on the same table but kept giving errors as I used the same alias 'T1' for it in each join
-- Solution - Use Notes.Friend twice BUT give it different aliases for each join to avoid an error. See below 


--__Model Answer Query__--


`
SELECT Sr.FirstName AS ScratcherName,
        Se.FirstName AS ScratcheeName,
        S.ScratchDate,
        S.ScratchTime
FROM Notes.Friends Sr
JOIN Notes.Scratched S ON Sr.FriendID = S.ScratcherID
JOIN Notes.Friends Se ON Se.FriendID = S.ScratcheeID
ORDER BY ScratchDate;
`

-- __Ch. 3 Textook Practice__ --

`
Select FriendID, PetDOB
From Notes.Pets 
Group By FriendID, PetDOB
`

-- GROUP BY groups __Rows__ -- 

-- None of the other cols in the table aboove are atomic after the grouping ---

-- so they run errors if you try to view them with SELECT --`

-- You can't select any cols not par of the GROUP BY clause ---

`
SELECT *--Gender
FROM Notes.RandomPeople
GROUP BY Gender
`


-- When SELECT is used to perform a function, a new column is usually formed so name it with AS '' --
-- SELECT also used to rename columns --

`
SELECT Gender, STDEV (Age) AS [SD Age]
FROM Notes.RandomPeople
GROUP BY Gender
`


--Other agg fxns --

`
SELECT Gender, 
        MIN (PersonName) AS [First Person in Row],
        MAX (PersonName) AS [Second Person in Row]
FROM Notes.RandomPeople
GROUP BY Gender
`

-- Use COUNT (*) to count all grouped rows, if not will skip NULL values ---

`
SELECT count(*)
FROM notes.Friends
GROUP BY FavColour
`

`
SELECT Gender, COUNT(Distinct Gender) AS 'Distinct Gender'
FROM Notes.RandomPeople
GROUP BY Gender
`

`
SELECT *
FROM Notes.RandomPeople --Letters
`

`
SELECT A, COUNT(DISTINCT CONCAT(A, B, Num)) AS NumAB  --
FROM Notes.Letters
GROUP BY A
`

-- CONCAT makes functions work across columns --

-- Aggregation functions generally return the same data type as the column they are applied to --

`
SELECT Gender, AVG (Age) AS [Average Age]
FROM Notes.RandomPeople
GROUP BY Gender
`


`
SELECT Gender,
        AVG (Age) AS AvAge, 
        AVG(CAST(Age AS DECIMAL(5,2))) AS AverageAge 
FROM notes.RandomPeople
GROUP BY Gender 
ORDER BY AverageAge
`


-- Integers give integer results, decimals may be lost so use CAST to change the type of data --


`
SELECT CASE WHEN PersonName LIKE 'B%' THEN 'B people'
            ELSE 'non-B people' END AS NameGroup,
            COUNT(*) AS NumPeople
FROM Notes.RandomPeople
GROUP BY CASE WHEN PersonName LIKE 'B%' THEN 'B people'
              ELSE 'non-B people' END;
`

`
SELECT Gender, AVG(Age) AS AverageAge
FROM Notes.RandomPeople
GROUP BY Gender
HAVING AVG(Age) > 40;
`

--HAVING works for grouped (aggregated) data, WHERE does not --


-- __Exercise 3.6.1__ --


`
SELECT A, B, MAX(Num) AS MaxNum, MIN(Num) AS MinNum
FROM Notes.Letters
GROUP BY A,B;
`


-- Order of Execution - FROM, WHERE, GROUP BY, HAVING, SELECT, ORDER BY --


-- 3a) error cause col FavColour is not in the GROUP BY clause. "FirstName' and other cols now are non-atomic (contain tuple entries) so won't give any result

-- 3b) gives all colours. Surprised null is still in the table. Okay, COUNT does not include NULL, but GROUP BY does

-- 3c) gives an eror. An aggregate fxn (in this case 'AVG') may not appear in the WHERE clause unless it is in a subquery contained in a HAVING clause or a SELECT list
-- i.e. __Aggregate functions must be used in HAVING or SELECT, not WHERE__

-- 3d) gives error. After using GROUP BY, there must be an aggregate fxn with the col name after HAVING clause OR the col must be specified in the GROUP BY clause, 
-- i.e. __No agg fxn should be used with WHERE__ 


`
SELECT AVG(Age) AS AvAge
FROM notes.RandomPeople
GROUP BY Gender
HAVING MAX(Age) > 20;
`

--- 3e)

`
SELECT Gender, MAX(Age) AS AgeMax, MIN(Age) AS AgeMin
FROM notes.RandomPeople
GROUP BY Gender
HAVING COUNT(*) < 3;
`

-- Gives the max and min ages of all genders that have less than three values in the aggregated row.

-- __Note__: Even if Age was not specified in the GROUP BY clause, it can be used with an aggregate fxn after SELECT and a new col created.


--- 3f) 

`
SELECT COUNT(*)
FROM Notes.RandomPeople;
`

-- Counts all the rows in the specified (Random People) table

-- 4) 


`
SELECT SaleDate, Product, Sales
FROM dbo.SausageSizzleSummary
ORDER BY SaleDate
`

-- Calculate the exact average number of sales for each SaleDate.

-- What is wrong with the query below??

`
SELECT SaleDate, AVG(Sales) AS AvgSales
FROM dbo.SausageSizzleSummary
GROUP BY SaleDate;
`

-- The 'AvgSales' results won't be 'exact' bcos it will produce integers, just like the original col 'Sales'. 
-- Which will be whole nos rounded down, even if the decimal is >.5


-- Write the right query --


`
SELECT SaleDate, AVG(CAST(Sales AS DECIMAL )) AS Avgsales
FROM dbo.SausageSizzleSummary
GROUP BY SaleDate;
`

-- CAST function used above to convert 'Sales' to decimals, so the results 'AvgSales' gives will be in decimals also --
-- __Note:__ No need to specify numbers after decimals --



