## Chapter 1: Exploring the Olympics Dataset
### Exercise 2: Athletes vs events by sport
Now consider the following visualization:

![](https://assets.datacamp.com/production/repositories/3815/datasets/4ce11f1e13f63d974bade7adc0e7250d7f8adf6e/1.1_e4.png)

Using the `summer_games` table, run a query that creates the base report that sources this visualization.

### Instructions for the exercises: 
- Pull a report that shows each sport, the number of unique events, and the number of unique athletes from the `summer_games` table.
- Group by the non-aggregated field, which is sport.

### Sample database:
![](https://i.ibb.co/wp0Q69Z/Capture-1.png)

### Query given as the solution: 
```sql
-- Query sport, events, and athletes from summer_games
SELECT 
	sport, 
    count(distinct(event)) AS events, 
    count(distinct(athlete_id)) AS athletes
FROM summer_games
GROUP BY sport;
```