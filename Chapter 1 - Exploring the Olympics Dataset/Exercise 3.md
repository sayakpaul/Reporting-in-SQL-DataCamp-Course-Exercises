## Chapter 1: Exploring the Olympics Dataset
### Exercise 3: Age of oldest athlete by region
You are given the following E:R diagram:

![](https://assets.datacamp.com/production/repositories/3815/datasets/07c3bd49158ae40e74674ed1afddcef9019ffb49/1.2_e1_a.png)

In the previous exercise, you identified which tables are needed to create a report that shows Age of Oldest Athlete by Region. Now, set up the query to create this report.

### Instructions for the exercises: 
- Create a report that shows region and age_of_oldest_athlete.
- Include all three tables by running two separate JOIN statements.
- Group by the non-aggregated field.
- It is highly suggested to alias tables.

### Sample database:
![](https://i.ibb.co/wp0Q69Z/Capture-1.png)

![](https://i.ibb.co/dmVVFh1/Capture-2.png)

![](https://i.ibb.co/pKzN99p/Capture-3.png)

![](https://i.ibb.co/tb6Krtg/Capture-4.png)

### Query given as the solution: 
```sql
-- Select the age of the oldest athlete for each region
SELECT 
	region, 
    max(c1.age) AS age_of_oldest_athlete
FROM athletes as c1
-- First JOIN statement
JOIN summer_games as c2
ON c1.id = c2.athlete_id
-- Second JOIN statement
JOIN countries c3
ON c2.country_id = c3.id
GROUP BY region;
```