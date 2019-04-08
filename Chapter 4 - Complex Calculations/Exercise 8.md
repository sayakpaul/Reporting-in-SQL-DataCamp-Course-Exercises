## Chapter 4: Complex Calculations
### Exercise 8: Report 4: Tallest athletes and % GDP by region
The final report on the dashboard is Report 4: Avg Tallest Athlete and % of world GDP by Region.

Report Details:

- Column 1 should be region found in the countries table.
- Column 2 should be avg_tallest, which averages the tallest athlete from each country within the region.
- Column 3 should be perc_world_gdp, which represents what % of the world's GDP is attributed to the region.
- GDP should only be counted from years 2005 and on.
- Only winter_games should be included (no summer events).

### Instructions for the exercises: 
- **Query 1**:
    - Pull country_id and height for winter athletes, group by these two fields, and order by country_id and height in descending order.
    - Use ROW_NUMBER() to create row_num, which numbers rows within a country by height where 1 is the tallest.
- **Query 2**:
    - Alias your query as subquery then use this subquery to join the countries table to pull in the region and average_tallest field, the last of which averages the tallest height of each country.
- **Query 3**:
    - Join to the country_stats table to create the perc_world_gdp field that calculates [region's GDP] / [world's GDP].

### Sample database:

![](https://camo.githubusercontent.com/32fc2a344bed1bb34e3910afd4cc85d00a2f9987/68747470733a2f2f692e6962622e636f2f704b7a4e3939702f436170747572652d332e706e67)

![](https://camo.githubusercontent.com/bc312c3142ed9abaeda617b00c4aac10382906ce/68747470733a2f2f692e6962622e636f2f564e534e7146462f436170747572652d352e706e67)

![](https://camo.githubusercontent.com/2eeb4b9f8be1109ec87e0da6ca16ff85bc57b21a/68747470733a2f2f692e6962622e636f2f7462364b7274672f436170747572652d342e706e67)

![](https://camo.githubusercontent.com/b031568d9ac99edddb3aed1263ebf10ac3098e61/68747470733a2f2f692e6962622e636f2f646d56564668312f436170747572652d322e706e67)

### Query given as the solution: 

* **Query 1**:
```sql
SELECT 
	-- Pull in country_id and height
	country_id,
    height,
    -- Number the height of each country's athletes
    ROW_NUMBER() OVER(PARTITION BY country_id) AS row_num
FROM winter_games
JOIN athletes
ON winter_games.athlete_id = athletes.id
GROUP BY country_id, height
-- Order by country_id and then height in descending order
ORDER BY country_id, height DESC;
```

* **Query 2**:
```sql
SELECT
	-- Pull in region and calculate avg tallest height
	region,
    avg(height) AS avg_tallest
FROM countries
JOIN
    (SELECT 
   	    -- Pull in country_id and height
        country_id, 
        height, 
        -- Number the height of each country's athletes
        ROW_NUMBER() OVER (PARTITION BY country_id ORDER BY height DESC) AS row_num
    FROM winter_games AS w 
    JOIN athletes AS a 
    ON w.athlete_id = a.id
    GROUP BY country_id, height
    -- Alias as subquery
    ORDER BY country_id, height DESC) AS subquery
ON countries.id = subquery.country_id
-- Only include the tallest height for each country
where row_num = 1
GROUP BY region;
```
* **Query 3**:
```sql
SELECT
	-- Pull in region and calculate avg tallest height
    region,
    AVG(height) AS avg_tallest,
    -- Calculate region's percent of world gdp
    SUM(gdp)/SUM(SUM(gdp)) OVER () AS perc_world_gdp    
FROM countries AS c
JOIN
    (SELECT 
     	-- Pull in country_id and height
        country_id, 
        height, 
        -- Number the height of each country's athletes
        ROW_NUMBER() OVER (PARTITION BY country_id ORDER BY height DESC) AS row_num
    FROM winter_games AS w 
    JOIN athletes AS a ON w.athlete_id = a.id
    GROUP BY country_id, height
    -- Alias as subquery
    ORDER BY country_id, height DESC) AS subquery
ON c.id = subquery.country_id
-- Join to country_stats
JOIN country_stats AS cs 
ON cs.country_id = c.id
-- Only include the tallest height for each country
WHERE row_num = 1
GROUP BY region;
```