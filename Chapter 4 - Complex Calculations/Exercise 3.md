## Chapter 4: Complex Calculations
### Exercise 3: Most decorated athlete per region
Your goal for this exercise is to show the most decorated athlete per region. To set up this report, you need to leverage the ROW_NUMBER() window function, which numbers each row as an incremental integer, where the first row is 1, the second is 2, and so on.

Syntax for this window function is ROW_NUMBER() OVER (PARTITION BY field ORDER BY field). Notice how there is no argument within the initial function.

When set up correctly, a row_num = 1 represents the most decorated athlete within that region. Note that you cannot use a window calculation within a HAVING or WHERE statement, so you will need to use a subquery to filter.

Feel free to reference the [E:R Diagram](https://assets.datacamp.com/production/repositories/3815/datasets/ed6586166b9158f3bc66814cb40b059ace13667d/ER_diagram_pdf.png). We will use summer_games_clean to avoid null handling.

### Instructions for the exercises: 
- Query 1: 
    - Build a query that pulls region, athlete_name, and total_golds by joining summer_games_clean, athletes, and countries.
    - Add a field called row_num that uses ROW_NUMBER() to assign a regional rank to each athlete based on total golds won.

- Query 2: 
    - Alias the subquery as subquery
    - Query region, athlete_name, and total_golds, and then filter for only the top athlete per region.

### Sample database:

![](https://camo.githubusercontent.com/2eeb4b9f8be1109ec87e0da6ca16ff85bc57b21a/68747470733a2f2f692e6962622e636f2f7462364b7274672f436170747572652d342e706e67)

![](https://i.ibb.co/tp7VpVd/Capture-1.png)

![](https://camo.githubusercontent.com/b031568d9ac99edddb3aed1263ebf10ac3098e61/68747470733a2f2f692e6962622e636f2f646d56564668312f436170747572652d322e706e67)

### Query given as the solution: 
**Query 1**:
```sql
SELECT 
	-- Query region, country, and total gold medals
	region, 
    name AS athlete_name, 
    SUM(gold) AS total_golds,
    -- Assign a regional rank to each athlete
    ROW_NUMBER() OVER (PARTITION by region ORDER BY SUM(gold) DESC) AS row_num
FROM summer_games_clean 
JOIN countries
ON summer_games_clean.country_id = countries.id
JOIN athletes
ON summer_games_clean.athlete_id = athletes.id
GROUP BY region, athlete_name;
```
**Query 2**:
```sql
-- Query region, athlete name, and total_golds
SELECT 
	region,
    athlete_name,
    total_golds
FROM
    (SELECT 
        -- Query region, country, and total gold medals
        region, 
        name AS athlete_name, 
        SUM(gold) AS total_golds,
        -- Assign a regional rank to each athlete
        ROW_NUMBER() OVER (PARTITION BY region ORDER BY SUM(gold) DESC) AS row_num
    FROM summer_games_clean AS s
    JOIN athletes AS a
    ON a.id = s.athlete_id
    JOIN countries AS c
    ON s.country_id = c.id
    -- Alias as subquery
    GROUP BY region, athlete_name) AS subquery
-- Filter for only the top athlete per region
WHERE row_num = 1;
```