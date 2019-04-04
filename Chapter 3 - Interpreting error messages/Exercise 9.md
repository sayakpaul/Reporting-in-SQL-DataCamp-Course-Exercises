## Chapter 3: Cleaning & Validation
### Exercise 9: Fixing calculations with coalesce
Null values impact aggregations in a number of ways. One issue is related to the AVG() function. By default, the AVG() function does not take into account any null values. However, there may be times when you want to include these null values in the calculation as zeros.

To replace null values with a string or a number, use the COALESCE() function. Syntax is COALESCE(fieldName,replacement), where replacement is what should replace all null instances of fieldName.

This exercise will walk you through why null values can throw off calculations and how to troubleshoot these issues.

### Instructions for the exercises: 
- Query 1: 
    - Build a report that shows total_events and gold_medals by athlete_id for all summer events, ordered by total_events descending then athlete_id ascending.
- Query 2:
    - Create a field called avg_golds that averages the gold field.
- Query 3:
    - Fix the avg_golds field be replacing null values with zero.

### Sample database:

![](https://camo.githubusercontent.com/fb54a3045fc8f79c2a2613e944be3e4709349b9d/68747470733a2f2f692e6962622e636f2f7770305136395a2f436170747572652d312e706e67)

![](https://camo.githubusercontent.com/b031568d9ac99edddb3aed1263ebf10ac3098e61/68747470733a2f2f692e6962622e636f2f646d56564668312f436170747572652d322e706e67)

### Query given as the solution: 
**Query 1**:
```sql
-- Pull events and golds by athlete_id for summer events
SELECT 
    athlete_id,
    COUNT(event) AS total_events, 
    SUM(gold) AS gold_medals
FROM summer_games
GROUP BY athlete_id
-- Order by total_events descending and athlete_id ascending
ORDER BY total_events desc, athlete_id asc;
```
**Query 2**:
```sql
-- Pull events and golds by athlete_id for summer events
SELECT 
    athlete_id, 
    -- Add a field that averages the existing gold field
    AVG(gold) AS avg_golds,
    COUNT(event) AS total_events, 
    SUM(gold) AS gold_medals
FROM summer_games AS s
GROUP BY athlete_id
-- Order by total_events descending and athlete_id ascending
ORDER BY total_events DESC, athlete_id;
```
**Query 3**: 
```sql
-- Pull events and golds by athlete_id for summer events
SELECT 
    athlete_id, 
    -- Replace all null gold values with 0
    AVG(COALESCE(gold, 0)) AS avg_golds,
    COUNT(event) AS total_events, 
    SUM(gold) AS gold_medals
FROM summer_games AS s
GROUP BY athlete_id
-- Order by total_events descending and athlete_id ascending
ORDER BY total_events DESC, athlete_id;
```