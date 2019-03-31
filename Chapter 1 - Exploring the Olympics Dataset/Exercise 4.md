## Chapter 1: Exploring the Olympics Dataset
### Exercise 4: Number of events in each sport
The full E:R diagram for the database is shown below:

![](https://assets.datacamp.com/production/repositories/3815/datasets/8243a439b44b3a6ddd4ca09a344331c47e266812/ER_diagram_dark.png)

Since the company will be involved in both summer sports and winter sports, it is beneficial to look at all sports in one centralized report.

Your task is to create a query that shows the unique number of events held for each sport. Note that since no relationships exist between these two tables, you will need to use a UNION instead of a JOIN.

### Instructions for the exercises: 
- Create a report that shows unique events by sport for both summer and winter events.
- Use a UNION to combine the relevant tables.
- Use two GROUP BY statements as needed.
- Order the final query to show the highest number of events first.

### Sample database:
![](https://i.ibb.co/wp0Q69Z/Capture-1.png)

![](https://i.ibb.co/VNSNqFF/Capture-5.png)

![](https://i.ibb.co/dmVVFh1/Capture-2.png)

![](https://i.ibb.co/pKzN99p/Capture-3.png)

![](https://i.ibb.co/tb6Krtg/Capture-4.png)

### Query given as the solution: 
```sql
-- Select sport and events for summer sports
SELECT 
	sport, 
    count(distinct(event)) as events
FROM summer_games
group by sport
UNION
-- Select sport and events for winter sports
SELECT 
	sport, 
    count(distinct(event)) as events
FROM winter_games
group by sport
-- Show the most athletes at the top of the report
order by sport;
```