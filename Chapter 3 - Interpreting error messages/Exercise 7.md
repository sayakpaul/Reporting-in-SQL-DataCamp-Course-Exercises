## Chapter 3: Cleaning & Validation
### Exercise 7: Fixing incorrect groupings
One issues with having strings stored in different formats is that you may incorrectly group data. If the same value is represented in multiple ways, your report will split the values into different rows, which can lead to inaccurate conclusions.

In this exercise, you will query from the summer_games_messy table, which is a messy, smaller version of summer_games. You'll notice that the same event is stored in multiple ways. Your job is to clean the event field to show the correct number of rows.

### Instructions for the exercises: 
- Query 1: 
    - Create a query that pulls the number of distinct athletes by event from the table summer_games_messy.
    - Group by the non-aggregated field.
- Query 2:
    - Notice how we see 6 rows that relate to only 2 events. Alter the event field by trimming all leading and trailing spaces, alias as event_fixed, and update the GROUP BY accordingly.
- Query 3:
    - Notice how there are now only 4 rows. Alter the event_fixed field further by removing all dashes (-).

### Sample database:

![](https://i.ibb.co/Q8Z0Z2g/Capture.png)

### Query given as the solution: 
**Query 1**:
```sql
-- Pull event and unique athletes from summer_games_messy 
SELECT 
	event, 
    count(distinct(athlete_id)) AS athletes
FROM summer_games_messy
-- Group by the non-aggregated field
GROUP BY event;
```
**Query 2**:
```sql
-- Pull event and unique athletes from summer_games_messy 
SELECT
    -- Remove trailing spaces and alias as event_fixed
	TRIM(event) as event_fixed, 
    COUNT(DISTINCT athlete_id) AS athletes
FROM summer_games_messy
-- Update the group by accordingly
GROUP BY event_fixed;
```
**Query 3**: 
```sql
-- Pull event and unique athletes from summer_games_messy 
SELECT 
    -- Remove dashes from all event values
    REPLACE(TRIM(event), '-', '') AS event_fixed, 
    COUNT(DISTINCT athlete_id) AS athletes
FROM summer_games_messy
-- Update the group by accordingly
GROUP BY event_fixed;
```