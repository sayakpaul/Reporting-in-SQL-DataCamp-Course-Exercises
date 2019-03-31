## Chapter 2: Creating Reports
### Exercise 9: Report 2: Top athletes in nobel-prized countries
It's time to bring together all the concepts brought up in this chapter to expand on your dashboard! Your next report to build is Report 2: Athletes Representing Nobel-Prize Winning Countries.

Report Details:
- Column 1 should be event, which represents the Olympic event. Both summer and winter events should be included.
- Column 2 should be gender, which represents the gender of athletes in the event.
- Column 3 should be athletes, which represents the unique athletes in the event.
- Athletes from countries that have had no nobel_prize_winners should be excluded.
- The report should contain 10 events, where events with the most athletes show at the top.

Click to view the [E:R Diagram](https://assets.datacamp.com/production/repositories/3815/datasets/ed6586166b9158f3bc66814cb40b059ace13667d/ER_diagram_pdf.png).

### Instructions for the exercises: 
- Select event from the summer_games table and create the athletes field by counting the distinct number of athlete_id.
- Explore the event field to determine how to split up events by gender (without adding a join), then add the gender field by using a CASE statement that specifies a conditional for 'female' events (all other events should output as 'male').
- Filter for Nobel-prize-winning countries by creating a subquery that outputs country_id from the country_stats table for any country with more than zero nobel_prize_winners.
- Copy your query with summer_games replaced by winter_games, UNION the two tables together, and order the final report to show the 10 rows with the most athletes.

### Sample database:

![](https://camo.githubusercontent.com/32fc2a344bed1bb34e3910afd4cc85d00a2f9987/68747470733a2f2f692e6962622e636f2f704b7a4e3939702f436170747572652d332e706e67)

![](https://camo.githubusercontent.com/fb54a3045fc8f79c2a2613e944be3e4709349b9d/68747470733a2f2f692e6962622e636f2f7770305136395a2f436170747572652d312e706e67)

![](![](https://camo.githubusercontent.com/bc312c3142ed9abaeda617b00c4aac10382906ce/68747470733a2f2f692e6962622e636f2f564e534e7146462f436170747572652d352e706e67))

### Query given as the solution: 

* **Query 1**: 
```sql
-- Pull event and unique athletes from summer_games 
SELECT 	
	event,
	count(distinct(athlete_id)) AS athletes
FROM summer_games
GROUP BY event;
```

* **Query 2**: 
```sql
-- Pull event and unique athletes from summer_games 
SELECT 
	event, 
    -- Add the gender field below
    CASE WHEN event LIKE '%Women%' THEN 'female'
    ELSE 'male' END AS gender,
    COUNT(DISTINCT athlete_id) AS athletes
FROM summer_games
GROUP BY event;
```

* **Query 3**: 
```sql
-- Pull event and unique athletes from summer_games 
SELECT 
    event,
    -- Add the gender field below
    CASE WHEN event LIKE '%Women%' THEN 'female' 
    ELSE 'male' END AS gender,
    COUNT(DISTINCT athlete_id) AS athletes
FROM summer_games
-- Only include countries that won a nobel prize
WHERE country_id IN 
	(SELECT country_id
    FROM country_stats
    WHERE nobel_prize_winners > 0)
GROUP BY event;
```

* **Query 4**: 
```sql
-- Pull event and unique athletes from summer_games 
SELECT 
    event,
    -- Add the gender field below
    CASE WHEN event LIKE '%Women%' THEN 'female' 
    ELSE 'male' END AS gender,
    COUNT(DISTINCT athlete_id) AS athletes
FROM summer_games
-- Only include countries that won a nobel prize
WHERE country_id IN 
	(SELECT country_id 
    FROM country_stats 
    WHERE nobel_prize_winners > 0)
GROUP BY event
-- Add the second query below and combine with a UNION
UNION
-- Pull event and unique athletes from summer_games 
SELECT 
    event,
    -- Add the gender field below
    CASE WHEN event LIKE '%Women%' THEN 'female' 
    ELSE 'male' END AS gender,
    COUNT(DISTINCT athlete_id) AS athletes
FROM winter_games
-- Only include countries that won a nobel prize
WHERE country_id IN 
	(SELECT country_id 
    FROM country_stats 
    WHERE nobel_prize_winners > 0)
GROUP BY event
-- Order and limit the final output
ORDER BY athletes desc
LIMIT 10;
```