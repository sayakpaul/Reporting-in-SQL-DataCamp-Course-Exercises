## Chapter 3: Cleaning & Validation
### Exercise 8: Filtering out nulls
One way to deal with nulls is to simply filter them out. There are two important conditionals related to nulls:

IS NULL is true for any value that is null.
IS NOT NULL is true for any value that is not null. Note that a zero or a blank cell is not the same as a null.
These conditionals can be leveraged by several clauses, such as CASE statements, WHERE statements, and HAVING statements. In this exercise, you will learn how to filter out nulls using two separate techniques.

Feel free to reference the [E:R Diagram](https://assets.datacamp.com/production/repositories/3815/datasets/ed6586166b9158f3bc66814cb40b059ace13667d/ER_diagram_pdf.png).

### Instructions for the exercises: 
- Query 1: 
    - Setup a query that pulls country and total golds as gold_medals for all winter games.
    - Group by the non-aggregated field and order by gold_medals in descending order.
- Query 2:
    - Notice how null values appear at the top of the results. Remove these by adding a WHERE statement that filters out all rows with null gold values.
- Query 3:
    - We can do a similar filter using HAVING. Comment out the WHERE statement and add a HAVING statement that filters out countries with no gold medals.

### Sample database:

![](https://camo.githubusercontent.com/b031568d9ac99edddb3aed1263ebf10ac3098e61/68747470733a2f2f692e6962622e636f2f646d56564668312f436170747572652d322e706e67)

![](https://camo.githubusercontent.com/bc312c3142ed9abaeda617b00c4aac10382906ce/68747470733a2f2f692e6962622e636f2f564e534e7146462f436170747572652d352e706e67)

### Query given as the solution: 
**Query 1**:
```sql
-- Show total gold_medals by country
SELECT 
	country,
    SUM(gold) AS gold_medals
FROM countries
JOIN winter_games
ON countries.id = winter_games.country_id
GROUP BY country
-- Order by gold_medals in descending order
ORDER BY gold_medals;
```
**Query 2**:
```sql
-- Show total gold_medals by country
SELECT 
	country, 
    SUM(gold) AS gold_medals
FROM winter_games AS w
JOIN countries AS c
ON w.country_id = c.id
-- Removes any row with no gold medals
WHERE gold IS NOT NULL
GROUP BY country
-- Order by gold_medals in descending order
ORDER BY gold_medals DESC;
```
**Query 3**: 
```sql
-- Show total gold_medals by country
SELECT 
	country, 
    SUM(gold) AS gold_medals
FROM winter_games AS w
JOIN countries AS c
ON w.country_id = c.id
-- Comment out the WHERE statement
-- WHERE gold IS NOT NULL
GROUP BY country
-- Replace WHERE statement with equivalent HAVING statement
HAVING (SUM(gold)) IS NOT NULL
-- Order by gold_medals in descending order
ORDER BY gold_medals DESC;
```