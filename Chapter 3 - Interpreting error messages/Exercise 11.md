## Chapter 3: Cleaning & Validation
### Exercise 11: Fixing duplication through a JOIN
In the previous exercise, you set up a query that contained duplication. This exercise will remove the duplication. One approach to removing duplication is to change the JOIN logic by adding another field to the ON statement.

The final query from last exercise is shown in the console. Your job is to fix the duplication by updating the ON statement. Note that the total gold_medals value should be 47.

Feel free to reference the [E:R Diagram](https://assets.datacamp.com/production/repositories/3815/datasets/ed6586166b9158f3bc66814cb40b059ace13667d/ER_diagram_pdf.png).

### Instructions for the exercises: 
- Query 1: 
    - Update the ON statement in the subquery by adding a second field to JOIN on.
    - If an error occurs related to the new JOIN field, use a CAST() statement to fix it.

### Sample database:

![](https://camo.githubusercontent.com/32fc2a344bed1bb34e3910afd4cc85d00a2f9987/68747470733a2f2f692e6962622e636f2f704b7a4e3939702f436170747572652d332e706e67)

![](https://camo.githubusercontent.com/bc312c3142ed9abaeda617b00c4aac10382906ce/68747470733a2f2f692e6962622e636f2f564e534e7146462f436170747572652d352e706e67)

### Query given as the solution: 
**Query 1**:
```sql
SELECT SUM(gold_medals) AS gold_medals
FROM
	(SELECT 
     	w.country_id, 
     	SUM(gold) AS gold_medals, 
     	AVG(gdp) AS avg_gdp
    FROM winter_games AS w
    JOIN country_stats AS c
    -- Update the subquery to join on a second field
    ON c.country_id = w.country_id and CAST(w.year as date) = CAST(c.year as date)
    GROUP BY w.country_id) AS subquery;
```
