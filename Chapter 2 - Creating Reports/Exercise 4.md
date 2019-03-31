## Chapter 2: Creating Reports
### Exercise 4: CASE statement refresher

CASE statements are useful for grouping values into different buckets based on conditions you specify. Any row that fails to satisfy any condition will fall to the ELSE statement (or show as null if no ELSE statement exists).

In this exercise, your goal is to create the segment field that buckets an athlete into one of three segments:

Tall Female, which represents a female that is at least 175 centimeters tall.
Tall Male, which represents a male that is at least 190 centimeters tall.
Other
Each segment will need to reference the fields height and gender from the athletes table. Leverage CASE statements and conditional logic (such as AND/OR) to build this.

Remember that each line of a case statement looks like this: CASE WHEN {condition} THEN {output}

### Instructions for the exercises: 
- Update the CASE statement to output three values: Tall Female, Tall Male, and Other.

### Sample database:

![](https://camo.githubusercontent.com/2eeb4b9f8be1109ec87e0da6ca16ff85bc57b21a/68747470733a2f2f692e6962622e636f2f7462364b7274672f436170747572652d342e706e67)

### Query given as the solution: 
```sql
SELECT 
	name,
    -- Output 'Tall Female', 'Tall Male', or 'Other'
	CASE WHEN gender = 'F' and height >= 175 THEN 'Tall Female'
    WHEN gender = 'M' and height >= 190 THEN 'Tall Male'
    ELSE 'Other' END AS segment
FROM athletes;
```