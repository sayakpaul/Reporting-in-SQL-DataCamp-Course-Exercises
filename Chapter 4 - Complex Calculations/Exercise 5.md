## Chapter 4: Complex Calculations
### Exercise 5: GDP per capita performance index
A performance index calculation is a good way to compare efficiency metrics across groups. A performance index compares each row to a benchmark.

To run a performance index calculation, take the following steps:

- Create a window function that outputs the performance for the entire partition.
- Run a ratio that divides each row's performance to the performance of the entire partition.

In this exercise, you will calculate the gdp_per_million for each country relative to the entire world.

- `gdp_per_million = gdp / pop_in_millions`

You will reference the country_stats_cleaned table, which is a copy of country_stats without data type issues.

### Instructions for the exercises: 
- Query 1: 
    - Update the query to pull gdp_per_million by region and country from country_stats_clean.
    - Filter for the year 2016, order by gdp_per_million in descending order, and remove all null gdp values.
- Query 2: 
    - Add the field gdp_per_million_total that takes the total gdp_per_million for the entire world.
- Query 3:
    - Add the performance_index that divides the gdp_per_million calculation by the gdp_per_million_total calculation.

### Sample database:

![](https://camo.githubusercontent.com/b031568d9ac99edddb3aed1263ebf10ac3098e61/68747470733a2f2f692e6962622e636f2f646d56564668312f436170747572652d322e706e67)

![](https://i.ibb.co/CB6DnLd/Capture-2.png)

### Query given as the solution: 
**Query 1**:
```sql

-- Bring in region, country, and gdp_per_million
SELECT 
    region,
    country,
    gdp/pop_in_millions AS gdp_per_million
-- Pull from country_stats_clean
FROM countries
JOIN country_stats_clean
ON countries.id = country_stats_clean.country_id
-- Filter for 2016 and remove null gdp values
WHERE date_part('year', year) = 2016 and gdp is not null
GROUP BY region, country, gdp_per_million
-- Show highest gdp_per_million at the top
ORDER BY gdp_per_million desc;
```
**Query 2**:
```sql
-- Bring in region, country, and gdp_per_million
SELECT 
    region,
    country,
    SUM(gdp) / SUM(pop_in_millions) AS gdp_per_million,
    -- Output the worlds gdp_per_million
    SUM(SUM(gdp)) OVER () / SUM(SUM(pop_in_millions)) OVER () AS gdp_per_million_total
-- Pull from country_stats_clean
FROM country_stats_clean AS cs
JOIN countries AS c 
ON cs.country_id = c.id
-- Filter for 2016 and remove null gdp values
WHERE year = '2016-01-01' AND gdp IS NOT NULL
GROUP BY region, country
-- Show highest gdp_per_million at the top
ORDER BY gdp_per_million DESC;
```
**Query 3**:
```sql
-- Bring in region, country, and gdp_per_million
SELECT 
    region,
    country,
    SUM(gdp) / SUM(pop_in_millions) AS gdp_per_million,
    -- Output the worlds gdp_per_million
    SUM(SUM(gdp)) OVER () / SUM(SUM(pop_in_millions)) OVER () AS gdp_per_million_total,
    -- Build the performance_index in the 3 lines below
    (SUM(gdp) / SUM(pop_in_millions))
    /
    (SUM(SUM(gdp)) OVER () / SUM(SUM(pop_in_millions)) OVER ()) AS performance_index
-- Pull from country_stats_clean
FROM country_stats_clean AS cs
JOIN countries AS c 
ON cs.country_id = c.id
-- Filter for 2016 and remove null gdp values
WHERE year = '2016-01-01' AND gdp IS NOT NULL
GROUP BY region, country
-- Show highest gdp_per_million at the top
ORDER BY gdp_per_million DESC;
```