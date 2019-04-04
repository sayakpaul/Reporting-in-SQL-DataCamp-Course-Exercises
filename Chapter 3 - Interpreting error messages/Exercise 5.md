## Chapter 3: Cleaning & Validation
### Exercise 5: Using date functions on strings
There are a number of string functions that can be used to alter strings. A description of a few of these functions are shown below:

- The LOWER(fieldName) function changes the case of all characters in fieldName to lower case.
- The INITCAP(fieldName) function changes the case of all characters in fieldName to proper case.
- The LEFT(fieldName,N) function returns the left N characters of the string fieldName.
- The SUBSTRING(fieldName from S for N) returns N characters starting from position S of the string fieldName. Note that both from S and for N are optional.

### Instructions for the exercises: 
- Update the field country_altered to output country in all lower-case.
- Update the field country_altered to output country in proper-case.
- Update the field country_altered to output country in proper-case.
- Update the field country_altered to output all characters starting with the 7th character of country.

### Sample database:

![](https://camo.githubusercontent.com/b031568d9ac99edddb3aed1263ebf10ac3098e61/68747470733a2f2f692e6962622e636f2f646d56564668312f436170747572652d322e706e67)

### Query given as the solution: 

```sql
-- Convert country to lower case
SELECT 
	country, 
    LOWER(country) AS country_altered
FROM countries
GROUP BY country;
```
