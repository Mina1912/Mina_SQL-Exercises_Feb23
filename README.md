# SQL_Feb23
NZSSN SQL training - February 2023

**I'm currently attending th NZSSN Feb '23 course taught by Daniel Fryer** 👩‍🎓
Fun but challenging so far 😥
Here's a copy of some of my coding exercises. Enjoy 😁

-- Exercise 2.7.1 --

-- 1. Retrieve only the names of all pets.
```Select *
From Notes.Pets
```
-- Columns are petID, petname, perDOB, FriendID

Select PetName
From Notes.Pets

--2. Retrieve the names of all pets that belong to the friend with FriendID
--equal to 3. Do not join any tables
Select PetName
From Notes.Pets 
Where FriendID = 3

--3. Display the first and last names of all friends whose favourite colour is red.
Select *
From Notes.Friends
-- Columns are FriendID, firstname, lastname, favcolor (I didn't pay attendtion to upper or lower case)

Select FirstName, lastname
From Notes.Friends
Where FavColour = 'red';
-- First attempt it gave only lastname column because I missed out the comma after firstname

--4. 
