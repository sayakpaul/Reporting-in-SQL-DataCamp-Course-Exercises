## Chapter 4: Complex Calculations
### Exercise 4: Percent of gdp per country
A percent of total calculation is a good way to compare volume metrics across groups. While simply showing the volume metric in a report provides some insights, adding a ratio allows us to easily compare values quickly.

To run a percent of total calculation, take the following steps:

- Create a window function that outputs the total volume, partitioned by whatever is considered the total. If the entire table is considered the total, then no partition clause is needed.
- Run a ratio that divides each row's volume metric by the total volume in the partition.

In this exercise, you will calculate the percent of gdp for each country relative to the entire world and relative to that country's region.

### Instructions for the exercises: 
- Query 1: 
    - Construct a query that pulls the country_gdp by region and country, order the query to show the highest country_gdp at the top, and then filter out all null gdp values.
- Query 2: 
    - Add the field global_gdp that outputs the total gdp across all countries.
- Query 3:
    - Create the field perc_global_gdp that calculates the percent of global gdp for the given country.
- Query 4:
    - Add the field perc_region_gdp, which runs the same calculation as perc_global_gdp but relative to each region.

### Sample database:

![](https://camo.githubusercontent.com/32fc2a344bed1bb34e3910afd4cc85d00a2f9987/68747470733a2f2f692e6962622e636f2f704b7a4e3939702f436170747572652d332e706e67)

![](https://camo.githubusercontent.com/b031568d9ac99edddb3aed1263ebf10ac3098e61/68747470733a2f2f692e6962622e636f2f646d56564668312f436170747572652d322e706e67)

### Query given as the solution: 
**Query 1**:
```sql
-- Pull country_gdp by region and country
SELECT 
	region,
    country,
	SUM(gdp) AS country_gdp
FROM countries
JOIN country_stats
ON countries.id = country_stats.country_id
-- Filter out null gdp values
WHERE gdp IS NOT NULL
GROUP BY region, country
-- Show the highest country_gdp at the top
ORDER BY country_gdp desc;
```
**Query 2**:
```sql
-- Pull country_gdp by region and country
SELECT 
	region,
    country,
	SUM(gdp) AS country_gdp,
    -- Calculate the global gdp
    SUM(SUM(gdp)) OVER () AS global_gdp
FROM country_stats AS cs
JOIN countries AS c
ON cs.country_id = c.id
-- Filter out null gdp values
WHERE gdp IS NOT NULL
GROUP BY region, country
-- Show the highest country_gdp at the top
ORDER BY country_gdp DESC;
```
**Query 3**:
```sql
-- Pull country_gdp by region and country
SELECT 
	region,
    country,
	SUM(gdp) AS country_gdp,
    -- Calculate the global gdp
    SUM(SUM(gdp)) OVER () AS global_gdp,
    -- Calculate percent of global gdp
    SUM(gdp)/SUM(SUM(gdp)) OVER () AS perc_global_gdp
FROM country_stats AS cs
JOIN countries AS c
ON cs.country_id = c.id
-- Filter out null gdp values
WHERE gdp IS NOT NULL
GROUP BY region, country
-- Show the highest country_gdp at the top
ORDER BY country_gdp DESC;
```
**Query 4**:
```sql
-- Pull country_gdp by region and country
SELECT 
	region,
    country,
	SUM(gdp) AS country_gdp,
    -- Calculate the global gdp
    SUM(SUM(gdp)) OVER () AS global_gdp,
    -- Calculate percent of global gdp
    SUM(gdp) / SUM(SUM(gdp)) OVER () AS perc_global_gdp,
    -- Calculate percent of gdp relative to its region
    SUM(gdp) / SUM(SUM(gdp)) OVER (PARTITION BY region) AS perc_region_gdp
FROM country_stats AS cs
JOIN countries AS c
ON cs.country_id = c.id
-- Filter out null gdp values
WHERE gdp IS NOT NULL
GROUP BY region, country
-- Show the highest country_gdp at the top
ORDER BY country_gdp DESC;
```