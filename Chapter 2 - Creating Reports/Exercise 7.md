## Chapter 2: Creating Reports
### Exercise 7: Filtering with a JOIN
When adding a filter to a query that requires you to reference a separate table, there are different approaches you can take. One option is to JOIN to the new table and then add a basic WHERE statement.

Your goal is to create a report with the following characteristics:
- First column is bronze_medals, or the total number of bronze.
- Second column is silver_medals, or the total number of silver.
- Third column is gold_medals, or the total number of gold.
- Only summer_games are included.
- Report is filtered to only include athletes age 16 or under.

In this exercise, use the JOIN approach.

### Instructions for the exercises: 
- Create a query that pulls total bronze_medals, silver_medals, and gold_medals from summer_games.
- Use a JOIN and a WHERE statement to filter for athletes ages 16 and below.

### Sample database:

![](https://camo.githubusercontent.com/2eeb4b9f8be1109ec87e0da6ca16ff85bc57b21a/68747470733a2f2f692e6962622e636f2f7462364b7274672f436170747572652d342e706e67)

![](https://camo.githubusercontent.com/fb54a3045fc8f79c2a2613e944be3e4709349b9d/68747470733a2f2f692e6962622e636f2f7770305136395a2f436170747572652d312e706e67)

### Query given as the solution: 
```sql
-- Pull summer bronze_medals, silver_medals, and gold_medals
SELECT 
	count(bronze) as bronze_medals, 
    count(silver) as silver_medals, 
    count(gold) as gold_medals
FROM summer_games
JOIN athletes
ON summer_games.athlete_id = athletes.id
-- Filter for athletes age 16 or below
WHERE age <= 16;
```