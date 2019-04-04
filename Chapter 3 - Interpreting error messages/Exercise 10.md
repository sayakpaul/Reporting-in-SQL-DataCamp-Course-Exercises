## Chapter 3: Cleaning & Validation
### Exercise 10: Identifying duplication
Duplication can happen for a number of reasons, often in unexpected ways. Because of this, it's important to get in the habit of validating your queries to ensure no duplication exists. To validate a query, take the following steps:

    1. Check the total value of a metric from the original table.
    2. Compare that with the total value of the same metric in your final report.

If the number from step 2 is larger than step 1, then duplication is likely the culprit. In this exercise, you will go through these steps to identify if duplication exists.

### Instructions for the exercises: 
- Query 1: 
    - Setup a query that pulls total gold_medals from the winter_games table.
- Query 2:
    - Comment out the top query after noting the gold_medals value.
    - Build a query that shows gold_medals and avg_gdp by country_id, but joins winter_games and country_stats only on the country_id fields.
- Query 3:
    - Wrap your newest query in a subquery, alias as subquery, and calculate the total value for the gold_medals field.

### Sample database:

![](https://camo.githubusercontent.com/32fc2a344bed1bb34e3910afd4cc85d00a2f9987/68747470733a2f2f692e6962622e636f2f704b7a4e3939702f436170747572652d332e706e67)

![](https://camo.githubusercontent.com/bc312c3142ed9abaeda617b00c4aac10382906ce/68747470733a2f2f692e6962622e636f2f564e534e7146462f436170747572652d352e706e67)

### Query given as the solution: 
**Query 1**:
```sql
-- Pull total gold_medals for winter sports
SELECT sum(gold) as gold_medals
FROM winter_games;
```
**Query 2**:
```sql
-- Show gold_medals and avg_gdp by country_id
SELECT 
	w.country_id, 
    SUM(gold) AS gold_medals, 
    AVG(gdp) AS avg_gdp
FROM winter_games w
JOIN country_stats c
-- Only join on the country_id fields
ON w.country_id = c.country_id
GROUP BY w.country_id;
```
**Query 3**: 
```sql
-- Calculate the total gold_medals in your query
SELECT sum(gold_medals)
FROM
	(SELECT 
        w.country_id, 
     	SUM(gold) AS gold_medals, 
        AVG(gdp) AS avg_gdp
    FROM winter_games AS w
    JOIN country_stats AS c
    ON c.country_id = w.country_id
    -- Alias your query as subquery
    GROUP BY w.country_id) AS subquery;
```