## Chapter 3: Cleaning & Validation
### Exercise 2: Interpreting error messages
Inevitably, you will run into errors when running SQL queries. It is important to understand how to interpret these errors to correctly identify what type of error it is.

The console contains two separate queries, each which will output an error when ran. In this exercise, you will run each query, read the error message, and troubleshoot the error.

### Instructions for the exercises: 
- Run the query in the console.
- After reading the error, fix it by converting the data type to float.
- Comment the first query and uncomment the second query.
- Run the code and fix errors by making the join columns int.

### Sample database:

![](https://camo.githubusercontent.com/32fc2a344bed1bb34e3910afd4cc85d00a2f9987/68747470733a2f2f692e6962622e636f2f704b7a4e3939702f436170747572652d332e706e67)

![](https://camo.githubusercontent.com/fb54a3045fc8f79c2a2613e944be3e4709349b9d/68747470733a2f2f692e6962622e636f2f7770305136395a2f436170747572652d312e706e67)

![](https://i.ibb.co/rmVtg2n/Capture-1.png)

### Query given as the solution: 

```sql
SELECT 
	s.country_id, 
    COUNT(DISTINCT s.athlete_id) AS summer_athletes, 
    COUNT(DISTINCT w.athlete_id) AS winter_athletes
FROM summer_games AS s
JOIN winter_games_str AS w
-- Fix the error by making both columns integers
ON CAST(s.country_id as int) = CAST(w.country_id as int)
GROUP BY s.country_id;
```