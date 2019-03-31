## Chapter 2: Creating Reports
### Exercise 3: UNION then JOIN query

Your goal is to create the same report as before, which contains with the following fields:

season, which outputs either summer or winter
country
events, which shows the unique number of events
In this exercise, create the query by using the UNION first, JOIN second approach. When taking this approach, you will need to use the initial UNION query as a subquery. The subquery will need to include all relevant fields, including those used in a join.

As always, feel free to reference the [E:R Diagram](https://assets.datacamp.com/production/repositories/3815/datasets/ed6586166b9158f3bc66814cb40b059ace13667d/ER_diagram_pdf.png).

### Instructions for the exercises: 
- In the parenthesis, construct a query that outputs season, country_id and event by combining summer and winter games with a UNION ALL and alias query as subquery.
- Leverage a JOIN and another SELECT statement to show the fields season, country and unique events.
- GROUP BY any unaggregated fields.
- Sort the report by events in descending order.

### Sample database:

![](https://camo.githubusercontent.com/b031568d9ac99edddb3aed1263ebf10ac3098e61/68747470733a2f2f692e6962622e636f2f646d56564668312f436170747572652d322e706e67)

![](https://camo.githubusercontent.com/fb54a3045fc8f79c2a2613e944be3e4709349b9d/68747470733a2f2f692e6962622e636f2f7770305136395a2f436170747572652d312e706e67)

![](https://camo.githubusercontent.com/bc312c3142ed9abaeda617b00c4aac10382906ce/68747470733a2f2f692e6962622e636f2f564e534e7146462f436170747572652d352e706e67)

### Query given as the solution: 
```sql
-- Add outer layer to pull season, country and unique events
SELECT 
	season, 
    country, 
    count(distinct(event)) AS events
FROM
    -- Pull season, country_id, and event for both seasons
    (SELECT 
     	'summer' AS season, 
     	country_id, 
     	event
    FROM summer_games
    UNION ALL
    SELECT 
     	'winter' AS season, 
     	country_id, 
     	event
    FROM winter_games) AS subquery
JOIN countries
ON subquery.country_id = countries.id
-- Group by any unaggregated fields
GROUP BY country, subquery.season
-- Order to show most events at the top
ORDER BY events;
```