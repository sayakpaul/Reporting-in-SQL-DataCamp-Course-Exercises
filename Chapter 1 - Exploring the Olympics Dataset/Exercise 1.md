## Chapter 1: Exploring the Olympics Dataset
### Exercise 1: Building the base report
Now, build the base report for this visualization:

![](https://assets.datacamp.com/production/repositories/3815/datasets/57127fe456ffc7a7445729435194b8754d7b63ce/1.1_e2.png)

This should be built by querying the summer_games table, found in the explorer on the bottom right.

### Instructions for the exercises: 
- Using the console on the right, select the sport field from the summer_games table.
- Create athletes by counting the distinct occurrences of athlete_id.
- Group by the sport field.
- Make the report only show 3 rows, with the highest athletes at the top.

### Sample database:
![](https://i.ibb.co/wp0Q69Z/Capture-1.png)

### Query given as the solution: 
```sql
-- Query the sport and distinct number of athletes
SELECT 
	sport, 
    count(distinct(athlete_id)) AS athletes
FROM summer_games
GROUP BY sport
-- Only include the 3 sports with the most athletes
ORDER BY sport desc
LIMIT 3;
```