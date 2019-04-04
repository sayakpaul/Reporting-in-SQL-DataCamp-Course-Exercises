## Chapter 3: Cleaning & Validation
### Exercise 12: Report 3: Countries with high medal rates
Great work so far! It is time to use the concepts you learned in this chapter to build the next base report for your dashboard.

Details for report 3: medals vs population rate.

- Column 1 should be country_code, which is an altered version of the country field.
- Column 2 should be pop_in_millions, representing the population of the country (in millions).
- Column 3 should be medals, representing the total number of medals.
- Column 4 should be medals_per_million, which equals medals / pop_in_millions

### Instructions for the exercises: 
- Query 1: 
    - Pull total medals by country for all summer games, where the medals field uses one SUM function and several null-handling functions on the gold, silver, and bronze fields.
- Query 2: 
    - Join to country_stats to pull in pop_in_millions, then create medals_per_million by dividing total medals by pop_in_millions and converting data types as needed.
- Query 3:
    - Notice the repeated values in the results. Add a column on the newest join statement to remove this duplication, and if you run into an error when trying to join, update the query so both fields are stored as type date.
- Query 4:
    - Update country to country_code by trimming leading spaces, converting to upper case, removing . characters, and keeping only the left 3 characters, then filter out null populations and keep only the 25 rows with the most medals_per_million.

### Sample database:

![](https://camo.githubusercontent.com/fb54a3045fc8f79c2a2613e944be3e4709349b9d/68747470733a2f2f692e6962622e636f2f7770305136395a2f436170747572652d312e706e67)

![](https://camo.githubusercontent.com/b031568d9ac99edddb3aed1263ebf10ac3098e61/68747470733a2f2f692e6962622e636f2f646d56564668312f436170747572652d322e706e67)

![](https://camo.githubusercontent.com/32fc2a344bed1bb34e3910afd4cc85d00a2f9987/68747470733a2f2f692e6962622e636f2f704b7a4e3939702f436170747572652d332e706e67)

### Query given as the solution: 
**Query 1**:
```sql
SELECT 
	c.country,
    -- Add the three medal fields using one sum function
	SUM(COALESCE(gold, 0) + COALESCE(silver, 0) + COALESCE(bronze, 0)) AS medals
FROM countries c
JOIN summer_games s
ON c.id = s.country_id
GROUP BY country
ORDER BY medals DESC;
```
**Query 2**:
```sql
SELECT 
	c.country,
    -- Pull in pop_in_millions and medals_per_million 
    pop_in_millions,
    -- Add the three medal fields using one sum function
	SUM(COALESCE(bronze,0) + COALESCE(silver,0) + COALESCE(gold,0)) AS medals,
    SUM(COALESCE(bronze,0) + COALESCE(silver,0) + COALESCE(gold,0))/CAST(cs.pop_in_millions AS float) AS medals_per_million
FROM summer_games AS s
JOIN countries AS c
ON s.country_id = c.id
-- Add a join
JOIN country_stats cs
ON c.id = cs.country_id
GROUP BY c.country, pop_in_millions
ORDER BY medals DESC;
```
**Query 3**:
```sql
SELECT 
	c.country,
    -- Pull in avg_pop_in_millions and medals_per_million 
	pop_in_millions,
    -- Add the three medal fields using one sum function
	SUM(COALESCE(bronze,0) + COALESCE(silver,0) + COALESCE(gold,0)) AS medals,
	SUM(COALESCE(bronze,0) + COALESCE(silver,0) + COALESCE(gold,0)) / CAST(cs.pop_in_millions AS float) AS medals_per_million
FROM summer_games AS s
JOIN countries AS c 
ON s.country_id = c.id
-- Update the newest join statement to remove duplication
JOIN country_stats AS cs 
ON s.country_id = cs.country_id and CAST(s.year as date) = CAST(cs.year as date)
GROUP BY c.country, pop_in_millions
ORDER BY medals DESC;
```
**Query 4**:
```sql
SELECT 
	-- Clean the country field to only show country_code
    TRIM(UPPER(LEFT(REPLACE(c.country,'.',''),3))) as country_code,
    -- Pull in avg_pop_in_millions and medals_per_million 
	pop_in_millions,
    -- Add the three medal fields using one sum function
	SUM(COALESCE(bronze,0) + COALESCE(silver,0) + COALESCE(gold,0)) AS medals,
	SUM(COALESCE(bronze,0) + COALESCE(silver,0) + COALESCE(gold,0)) / CAST(cs.pop_in_millions AS float) AS medals_per_million
FROM summer_games AS s
JOIN countries AS c 
ON s.country_id = c.id
-- Update the newest join statement to remove duplication
JOIN country_stats AS cs 
ON s.country_id = cs.country_id AND s.year = CAST(cs.year AS date)
-- Filter out null populations
WHERE cs.pop_in_millions IS NOT NULL
GROUP BY c.country, pop_in_millions
-- Keep only the top 25 medals_per_million rows
ORDER BY medals_per_million desc
LIMIT 25;
```