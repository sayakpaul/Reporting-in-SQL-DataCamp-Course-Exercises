## Chapter 4: Complex Calculations
### Exercise 1: Complex Calculations
Window functions reference other rows within the report. There are a variety of window-specific functions to use, but all basic aggregation functions can be used as a window function. These include:

- SUM()
- AVG()
- MAX()
- MIN()

The syntax of a window function is FUNCTION(value) OVER (PARTITION BY field ORDER BY field). Note that the PARTITION BY and ORDER BY clauses are optional. The FUNCTION should be replaced with the function of your choice.

In this exercise, you will run a few different window functions on the country_stats table.

### Instructions for the exercises: 
- Query 1: 
    - Add the field country_avg_gdp that outputs the average gdp for each country.
- Query 2: 
    - Change country_avg_gdp to country_sum_gdp that shows the total gdp for each country across all years.
- Query 3:
    - Change country_sum_gdp to country_max_gdp that shows the highest GDP for each country.
- Query 4:
    - Change country_max_gdp to global_max_gdp that shows the highest GDP value for the entire world.

### Sample database:

![](https://camo.githubusercontent.com/32fc2a344bed1bb34e3910afd4cc85d00a2f9987/68747470733a2f2f692e6962622e636f2f704b7a4e3939702f436170747572652d332e706e67)

### Query given as the solution: 
**Query 1**:
```sql
SELECT 
	country_id,
    year,
    gdp,
    -- Show the average gdp across all years per country
	AVG(gdp) OVER (PARTITION BY country_id) AS country_avg_gdp
FROM country_stats;
```
**Query 2**:
```sql
SELECT 
	country_id,
    year,
    gdp,
    -- Show total gdp per country and alias accordingly
	SUM(gdp) OVER (PARTITION BY country_id) AS country_sum_gdp
FROM country_stats;
```
**Query 3**:
```sql
SELECT 
	country_id,
    year,
    gdp,
    -- Show max gdp per country and alias accordingly
	MAX(gdp) OVER (PARTITION BY country_id) AS country_max_gdp
FROM country_stats;
```
**Query 4**:
```sql
SELECT 
	country_id,
    year,
    gdp,
    -- Show max gdp for the table and alias accordingly
	MAX(gdp) OVER () AS global_max_gdp
FROM country_stats;
```