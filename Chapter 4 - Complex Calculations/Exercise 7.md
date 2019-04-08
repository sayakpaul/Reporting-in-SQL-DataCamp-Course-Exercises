## Chapter 4: Complex Calculations
### Exercise 7: Week-over-week comparison
In the previous exercise, you leveraged the set window of a month to calculate month-over-month changes. But sometimes, you may want to calculate a different time period, such as comparing last 7 days to the previous 7 days. To calculate a value from the last 7 days, you will need to set up a rolling calculation.

In this exercise, you will take the rolling 7 day average of views for each date and compare it to the previous 7 day average for views. This gives a clear week-over-week comparison for every single day.

Syntax for a rolling average is `AVG(value) OVER (PARTITION BY field ORDER BY field ROWS BETWEEN N PRECEDING AND CURRENT ROW)`, where N is the number of rows to look back when doing the calculation. Remember that CURRENT ROW counts as a row.

### Instructions for the exercises: 
- **Query 1**:
   - Show daily_views and weekly_avg by date, where weekly_avg is the rolling 7 day average of views.
- **Query 2**:
    - Alias the query as subquery, add an outer layer that pulls date and weekly_avg, and order by date in descending order.
    - Create the field weekly_avg_previous that takes the weekly_avg from 7 days prior to the given date.
- **Query 3**:
    - Calculate perc_change where a value of 0 indicates no change, a negative value represents a drop in views versus previous period, and a positive value represents growth.

### Sample database:

![](https://i.ibb.co/Y8xNXP0/Capture.png)

### Query given as the solution: 

* **Query 1**:
```sql
SELECT
	-- Pull in date and daily_views
	date,
	SUM(views) AS daily_views,
    -- Calculate the rolling 7 day average
	AVG(SUM(views)) OVER (ORDER BY date ROWS BETWEEN 6 PRECEDING AND CURRENT ROW) AS weekly_avg
FROM web_data
GROUP BY date;
```

* **Query 2**:
```sql
SELECT 
	-- Pull in date and weekly_avg
	date,
    weekly_avg,
    -- Output the value of weekly_avg from 7 days prior
    LAG(weekly_avg, 7) OVER (ORDER BY date) AS weekly_avg_previous
FROM
  (SELECT
      -- Pull in date and daily_views
      date,
      SUM(views) AS daily_views,
      -- Calculate the rolling 7 day average
      AVG(SUM(views)) OVER (ORDER BY date ROWS BETWEEN 6 PRECEDING AND CURRENT ROW) AS weekly_avg
  FROM web_data
  -- Alias as subquery
  GROUP BY date) AS subquery
-- Order by date in descending order
ORDER BY date desc;
```
* **Query 3**:
```sql
SELECT 
	-- Pull in date and weekly_avg
	date,
    weekly_avg,
    -- Output the value of weekly_avg from 7 days prior
    LAG(weekly_avg,7) OVER (ORDER BY date) AS weekly_avg_previous,
    -- Calculate percent change vs previous period
    weekly_avg
    /
    LAG(weekly_avg,7) OVER (ORDER BY date) -1
    AS perc_change
FROM
  (SELECT
      -- Pull in date and daily_views
      date,
      SUM(views) AS daily_views,
      -- Calculate the rolling 7 day average
      AVG(SUM(views)) OVER (ORDER BY date ROWS BETWEEN 6 PRECEDING AND CURRENT ROW) AS weekly_avg
  FROM web_data
  -- Alias as subquery
  GROUP BY date) AS subquery
-- Order by date in descending order
ORDER BY date DESC;
```