## Chapter 3: Cleaning & Validation
### Exercise 3: Interpreting error messages
There are several useful functions that act specifically on date or datetime fields. For example:

- DATE_TRUNC('month', date) truncates each date to the first day of the month.
- DATE_PART('year', date) outputs the year, as an integer, of each date value.

In general, the arguments for both functions are ('period', field), where period is a date or time interval, such as 'minute', 'day', or 'decade'.

In this exercise, your goal is to test out these date functions on the country_stats table, specifically by outputting the decade of each year using two separate approaches. To run these functions, you will need to use CAST() function on the year field.

### Instructions for the exercises: 
- Pulling from the country_stats table, select the decade using two methods: DATE_PART() and DATE_TRUNC.
- Convert the data type of the year field to fix errors.
- Sum up gdp to get world_gdp.
- Group and order by year (in descending order).

### Sample database:

![](https://camo.githubusercontent.com/32fc2a344bed1bb34e3910afd4cc85d00a2f9987/68747470733a2f2f692e6962622e636f2f704b7a4e3939702f436170747572652d332e706e67)

### Query given as the solution: 

```sql
SELECT 
	year,
    -- Pull decade, decade_truncate, and the world's gdp
    DATE_PART('decade',CAST(year AS date)) AS decade,
    DATE_TRUNC('decade',CAST(year AS date)) AS decade_truncated,
    SUM(gdp) AS world_gdp
FROM country_stats
-- Group and order by year in descending order
GROUP BY year
ORDER BY year DESC;
```