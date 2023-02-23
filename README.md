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





