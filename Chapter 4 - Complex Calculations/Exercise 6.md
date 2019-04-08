## Chapter 4: Complex Calculations
### Exercise 6: Month-over-month comparison
In order to compare months, you need to use one of the following window functions:

- LAG(value, offset), which outputs a value from an offset number previous to to the current row in the report.
- LEAD(value, offset), which outputs a value from a offset number after the current row in the report.

Your goal is to build a report that shows each country's month-over-month views. A few tips:

- You will need to bucket dates into months. To do this, you can use the DATE_PART() function.
- You can calculate the percent change using the following formula: (value)/(previous_value) - 1.
- If no offset value is included in the LAG() or LEAD() functions, it will default to 1.

Since the table stops in the middle of June, the query is set up to only include data to the end of May.

### Instructions for the exercises: 
- From web_data, pull in country_id and use a DATE_PART() function to create month.
- Create month_views that pulls the total views within the month.
- Create previous_month_views that pulls the total views from last month for the given country.
- Create the field perc_change that calculates the percent change of this month relative to last month for the given country, where a negative value represents a loss in views and a positive value represents growth.


### Sample database:

![](https://i.ibb.co/Y8xNXP0/Capture.png)

### Query given as the solution: 
```sql
SELECT
	-- Pull month and country_id
	DATE_PART('month', date) AS month,
	country_id,
    -- Pull in current month views
    SUM(views) AS month_views,
    -- Pull in last month views
    LAG(SUM(views)) OVER (PARTITION BY country_id ORDER BY DATE_PART('month', date)) AS previous_month_views,
    -- Calculate the percent change
    SUM(views) / LAG(SUM(views)) OVER (PARTITION BY country_id ORDER BY DATE_PART('month', date)) - 1 AS perc_change
FROM web_data
WHERE date <= '2018-05-31'
GROUP BY month, country_id;
```