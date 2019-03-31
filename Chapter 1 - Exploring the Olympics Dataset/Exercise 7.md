## Chapter 1: Exploring the Olympics Dataset
### Exercise 7: Report 1: Most decorated summer athletes

Now that you have a good understanding of the data, let's get back to our case study and build out the first element for the dashboard, Most Decorated Summer Athletes:

![](https://assets.datacamp.com/production/repositories/3815/datasets/96ab53e9c29ad378084d8e2797037bc260cc4355/1.3_capstone_pic_b.png)

Your job is to create the base report for this element. Base report details:

Column 1 should be athlete_name.
Column 2 should be gold_medals.
The report should only include athletes with at least 3 medals.
The report should be ordered by gold medals won, with the most medals at the top.

### Instructions for the exercises: 
- Select athlete_name and gold_medals by joining summer_games and athletes.
- Only include athlete_name with at least 3 gold medals.
- Sort the table so that the most gold_medals appears at the top.

### Sample database:
![](https://i.ibb.co/wp0Q69Z/Capture-1.png)

![](https://i.ibb.co/dmVVFh1/Capture-2.png)

### Query given as the solution: 
```sql
-- Pull athlete_name and gold_medals for summer games
SELECT 
	a.name AS athlete_name, 
    sum(s.gold) AS gold_medals
FROM athletes a
JOIN summer_games s
ON a.id = s.athlete_id
GROUP BY athlete_name
-- Filter for only athletes with 3 gold medals or more
HAVING sum(s.gold) >= 3
-- Sort to show the most gold medals at the top
ORDER BY gold_medals;
```