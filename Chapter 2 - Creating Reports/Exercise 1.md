## Chapter 2: Creating Reports
### Exercise 1: Planning the filter

Your boss is looking to see which winter events include athletes over the age of 40. To answer this, you need a report that lists out all events that satisfy this condition. In order to have a correct list, you will need to leverage a filter. In this exercise, you will decide which filter option to use.

### Instructions for the exercises: 
- Create a query that shows all unique event names in the winter_games table.
- Only include athlete_name with at least 3 gold medals.
- Sort the table so that the most gold_medals appears at the top.

### Sample database:

![](https://camo.githubusercontent.com/bc312c3142ed9abaeda617b00c4aac10382906ce/68747470733a2f2f692e6962622e636f2f564e534e7146462f436170747572652d352e706e67)

### Query given as the solution: 
```sql
SELECT distinct(event)
FROM winter_games;
```