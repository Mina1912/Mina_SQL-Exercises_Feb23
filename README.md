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







