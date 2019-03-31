## Chapter 2: Creating Reports
### Exercise 2: JOIN then UNION query

Your goal is to create a report with the following fields:

season, which outputs either summer or winter
country
events, which shows the unique number of events
There are multiple ways to create this report. In this exercise, create the query by using the JOIN first, UNION second approach.

As always, feel free to reference your [E:R Diagram](https://assets.datacamp.com/production/repositories/3815/datasets/ed6586166b9158f3bc66814cb40b059ace13667d/ER_diagram_pdf.png) to identify relevant fields and tables.

### Instructions for the exercises: 
- Setup a query that shows unique events by country and season for summer events.
- Setup a similar query that shows unique events by country and season for winter events.
- Combine the two queries using a UNION ALL.
- Sort the report by events in descending order.

### Sample database:

![](https://camo.githubusercontent.com/b031568d9ac99edddb3aed1263ebf10ac3098e61/68747470733a2f2f692e6962622e636f2f646d56564668312f436170747572652d322e706e67)

![](https://camo.githubusercontent.com/fb54a3045fc8f79c2a2613e944be3e4709349b9d/68747470733a2f2f692e6962622e636f2f7770305136395a2f436170747572652d312e706e67)

![](https://camo.githubusercontent.com/bc312c3142ed9abaeda617b00c4aac10382906ce/68747470733a2f2f692e6962622e636f2f564e534e7146462f436170747572652d352e706e67)

### Query given as the solution: 
```sql
-- Query season, country, and events for all summer events
SELECT 
	'summer' AS season, 
    country, 
    count(distinct(event)) AS events
FROM summer_games
JOIN countries
ON summer_games.country_id = countries.id
GROUP BY countries.country
-- Combine the queries
UNION ALL
-- Query season, country, and events for all winter events
SELECT 
	'winter' AS season, 
    country, 
    count(distinct(winter_games.event)) AS events
FROM winter_games
JOIN countries
ON winter_games.country_id = countries.id
GROUP BY countries.country
-- Sort the results to show most events at the top
ORDER BY events;
```