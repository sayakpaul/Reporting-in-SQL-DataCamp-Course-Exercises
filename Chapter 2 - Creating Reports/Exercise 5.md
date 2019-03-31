## Chapter 2: Creating Reports
### Exercise 5: BMI bucket by sport

You are looking to understand how BMI differs by each summer sport. To answer this, set up a report that contains the following:

- sport, which is the name of the summer sport
- bmi_bucket, which splits up BMI into three groups: <.25, .25-.30, >.30
- athletes, or the unique number of athletes

Definition: BMI = 100 * weight / (height squared).

Also note that CASE statements run row-by-row, so the second conditional is only applied if the first conditional is false. This makes it that you do not need an AND statement excluding already-mentioned conditionals.

### Instructions for the exercises: 
- Build a query that pulls from summer_games and athletes to show sport, bmi_bucket, and athletes.
- Without using AND or ELSE, set up a CASE statement that splits bmi_bucket into three groups: '<.25', '.25-.30', and '>.30'.
- Group by the non-aggregated fields.
- Order the report by sport and then athletes in descending order.

### Sample database:

![](https://camo.githubusercontent.com/2eeb4b9f8be1109ec87e0da6ca16ff85bc57b21a/68747470733a2f2f692e6962622e636f2f7462364b7274672f436170747572652d342e706e67)

![](https://camo.githubusercontent.com/fb54a3045fc8f79c2a2613e944be3e4709349b9d/68747470733a2f2f692e6962622e636f2f7770305136395a2f436170747572652d312e706e67)

### Query given as the solution: 
```sql
-- Pull in sport, bmi_bucket, and athletes
SELECT 
	sport,
    -- Bucket BMI in three groups: <.25, .25-.30, and >.30	
    CASE WHEN weight/height^2*100 <.25 THEN '<.25'
    WHEN weight/height^2*100 <=.30 THEN '.25-.30'
    WHEN weight/height^2*100 >.30 THEN '>.30' END AS bmi_bucket,
    COUNT(DISTINCT athlete_id) AS athletes
FROM summer_games AS sg
JOIN athletes AS a
ON sg.athlete_id = a.id
-- GROUP BY non-aggregated fields
GROUP BY sport, bmi_bucket
-- Sort by sport and then by athletes in descending order
ORDER BY sport, athletes DESC;
```