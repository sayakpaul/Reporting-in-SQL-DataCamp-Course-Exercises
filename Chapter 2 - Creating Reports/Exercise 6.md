## Chapter 2: Creating Reports
### Exercise 6: Troubleshooting CASE statements
In the previous exercise, you may have noticed several null values in our case statement, which can indicate there is an issue with the code.

In these instances, it's worth investigating to understand why these null values are appearing. In this exercise, you will go through a series of steps to identify the issue and make changes to the code where necessary.

### Instructions for the exercises: 
- Comment out the troubleshooting query, uncomment the original query, and add an ELSE line to the CASE statement that outputs 'no weight recorded'.

### Sample database:

![](https://camo.githubusercontent.com/2eeb4b9f8be1109ec87e0da6ca16ff85bc57b21a/68747470733a2f2f692e6962622e636f2f7462364b7274672f436170747572652d342e706e67)

![](https://camo.githubusercontent.com/fb54a3045fc8f79c2a2613e944be3e4709349b9d/68747470733a2f2f692e6962622e636f2f7770305136395a2f436170747572652d312e706e67)

### Query given as the solution: 
```sql
-- Uncomment the original query
SELECT 
	sport,
    CASE WHEN weight/height^2*100 <.25 THEN '<.25'
    WHEN weight/height^2*100 <=.30 THEN '.25-.30'
    WHEN weight/height^2*100 >.30 THEN '>.30'
    -- Add ELSE statement to output 'no weight recorded'
    ELSE 'no weight recorded' END AS bmi_bucket,
    COUNT(DISTINCT athlete_id) AS athletes
FROM summer_games AS sg
JOIN athletes AS a
ON sg.athlete_id = a.id
GROUP BY sport, bmi_bucket
ORDER BY sport, athletes DESC;

/*-- Comment out the troubleshooting query
SELECT 
	height, 
    weight, 
    weight/height^2*100 AS bmi
FROM athletes
WHERE weight/height^2*100 IS NULL; */
```