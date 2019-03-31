## Chapter 2: Creating Reports
### Exercise 8: Filtering with a subquery
Another approach to filter from a separate table is to use a subquery. The process is as follows:

- Create a subquery that outputs a list.
- In your main query, add a WHERE statement that references the list.

Your goal is to create the same report as the last exercise, which contains the following characteristics:

- First column is bronze_medals, or the total number of bronze.
- Second column is silver_medals, or the total number of silver.
- Third column is gold_medals, or the total number of gold.
- Only summer_games are included.
- Report is filtered to only include athletes age 16 or under.

In this exercise, use the subquery approach.

### Instructions for the exercises: 
- Create a query that pulls total bronze_medals, silver_medals, and gold_medals from summer_games.
- Setup a subquery that outputs all athletes age 16 or below.
- Add a WHERE statement that references the subquery to filter for athletes age 16 or below.

### Sample database:

![](https://camo.githubusercontent.com/2eeb4b9f8be1109ec87e0da6ca16ff85bc57b21a/68747470733a2f2f692e6962622e636f2f7462364b7274672f436170747572652d342e706e67)

![](https://camo.githubusercontent.com/fb54a3045fc8f79c2a2613e944be3e4709349b9d/68747470733a2f2f692e6962622e636f2f7770305136395a2f436170747572652d312e706e67)

### Query given as the solution: 
```sql
-- Pull summer bronze_medals, silver_medals, and gold_medals
SELECT 
	sum(bronze) as bronze_medals, 
    sum(silver) as silver_medals, 
    sum(gold) as gold_medals
FROM summer_games
-- Add the WHERE statement below
WHERE athlete_id IN
    -- Create subquery list for athlete_ids age 16 or below    
    (SELECT id 
     FROM athletes
     WHERE age <= 16);
```