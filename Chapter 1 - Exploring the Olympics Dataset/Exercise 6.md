## Chapter 1: Exploring the Olympics Dataset
### Exercise 6: Validating our query

The same techniques we use to explore the data can be used to validate queries. By using the query as a subquery, you can run exploratory techniques to confirm the query results are as expected.

In this exercise, you will create a query that shows Bronze Medals by Country and then validate it using the subquery technique.

Feel free to reference the [E:R Diagram](https://assets.datacamp.com/production/repositories/3815/datasets/ed6586166b9158f3bc66814cb40b059ace13667d/ER_diagram_pdf.png) as needed.

### Instructions for the exercises: 
- Create a query that outputs total bronze medals from the summer_games table.
- The value for total_bronze_medals is commented out for reference. Setup a query that shows bronze_medals for summer_games by country.
- Add parenthesis to your query you just created and alias as subquery.
- Select the total number of bronze_medals and compare to the total bronze medals in summer_games.

### Sample database:
![](https://i.ibb.co/wp0Q69Z/Capture-1.png)

![](https://i.ibb.co/dmVVFh1/Capture-2.png)

### Query given as the solution: 
- **Query 1**: 
```sql
-- Pull total_bronze_medals from summer_games below
SELECT count(bronze) AS total_bronze_medals
FROM summer_games;
```
- **Query 2**: 
```sql
-- Setup a query that shows bronze_medal by country
SELECT 
	country, 
    SUM(bronze) AS bronze_medals
FROM countries
JOIN summer_games
ON countries.id = summer_games.country_id
GROUP BY country;
```
- **Query 3**: 
```sql
-- Select the total bronze_medals from your query
SELECT sum(bronze_medals)
FROM 
-- Previous query is shown below.  Alias this AS subquery
  (SELECT 
      country, 
      SUM(bronze) AS bronze_medals
  FROM summer_games AS s
  JOIN countries AS c
  ON s.country_id = c.id
  GROUP BY country) as subquery
;
```