## Chapter 1: Exploring the Olympics Dataset
### Exercise 4: Exploring `summer_games`

Exploring the data in a table can provide further insights into the database as a whole. In this exercise, you will try out a series of different techniques to explore the summer_games table.

### Instructions for the exercises: 
- Select bronze from the summer_games table, but do not use DISTINCT or GROUP BY.
- The results do not provide much insight as we mostly see NULL. Add a DISTINCT to only show unique bronze values.
- GROUP BY is an alternative to using DISTINCT. Remove the DISTINCT and add a GROUP BY statement.
- Let's see how much of our dataset is NULL. Add a field that shows number of rows to your query.

### Sample database:
![](https://i.ibb.co/wp0Q69Z/Capture-1.png)

### Query given as the solution: 
- **Query 1**: 
```sql
-- Update the query to explore the bronze field
SELECT bronze
FROM summer_games;
```
- **Query 2**: 
```sql
-- Update query to explore the unique bronze field values
SELECT DISTINCT(bronze)
FROM summer_games;
```
- **Query 3**: 
```sql
-- Recreate the query by using GROUP BY 
SELECT bronze
FROM summer_games
group by bronze;
```
- **Query 4**: 
```sql
-- Add the rows column to your query
SELECT 
	bronze, 
	count(*) AS rows
FROM summer_games
GROUP BY bronze;
```