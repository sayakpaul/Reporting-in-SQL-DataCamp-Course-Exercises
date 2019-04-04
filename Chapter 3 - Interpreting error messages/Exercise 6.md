## Chapter 3: Cleaning & Validation
### Exercise 6: Replacing and removing substrings
The REPLACE() function is a versatile function that allows you to replace or remove characters from a string. The syntax is as follows:

> REPLACE(fieldName, 'searchFor', 'replaceWith')

Where fieldName is the field or string being updated, searchFor is the characters to be replaced, and replaceWith is the replacement substring.

In this exercise, you will look at one specific value in the countries table and change up the format by using a few REPLACE() functions.

### Instructions for the exercises: 
- Query 1: 
    - Create the field character_swap that replaces all '&' characters with 'and' from region.
    - Create the field character_remove that removes all periods from region.
- Query 2:
    - Add a new field called character_swap_and_remove that runs the alterations of both   character_swap and character_remove in one go.

### Sample database:

![](https://camo.githubusercontent.com/b031568d9ac99edddb3aed1263ebf10ac3098e61/68747470733a2f2f692e6962622e636f2f646d56564668312f436170747572652d322e706e67)

### Query given as the solution: 
**Query 1**:
```sql
SELECT 
	region, 
    -- Replace all '&' characters with the string 'and'
    REPLACE(region,'&','and') AS character_swap,
    -- Remove all periods
    REPLACE(region,'.','') AS character_remove
FROM countries
WHERE region = 'LATIN AMER. & CARIB'
GROUP BY region;
```
**Query 2**:
```sql
SELECT 
	region, 
    -- Replace all '&' characters with the string 'and'
    REPLACE(region,'&','and') AS character_swap,
    -- Remove all periods
    REPLACE(region,'.','') AS character_remove,
    -- Combine the functions to run both changes at once
   REPLACE(REPLACE(region,'.',''), '&', 'and') AS character_swap_and_remove
FROM countries
WHERE region = 'LATIN AMER. & CARIB'
GROUP BY region;
```