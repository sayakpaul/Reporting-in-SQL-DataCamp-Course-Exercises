## Chapter 3: Cleaning & Validation
### Exercise 1: Identifying data types
Being able to identify data types before setting up your query can help you plan for any potential issues. There is a group of tables, or a schema, called the information_schema, which provides a wide array of information about the database itself, including the structure of tables and columns.

The columns table houses useful details about the columns, including the data type.

Note that the information_schema is not the default schema SQL looks at when querying, which means you will need to explicitly tell SQL to pull from this schema. To pull a table from a non-default schema, use the syntax schema_name.table_name.

### Instructions for the exercises: 
- Select the fields column_name and data_type from the table columns that resides within the information_schema schema.
- Filter only for the 'country_stats' table.

### Sample database:

![](https://camo.githubusercontent.com/32fc2a344bed1bb34e3910afd4cc85d00a2f9987/68747470733a2f2f692e6962622e636f2f704b7a4e3939702f436170747572652d332e706e67)

### Query given as the solution: 

```sql
-- Pull column_name & data_type from the columns table
SELECT 
	column_name,
    data_type
FROM information_schema.columns
-- Filter for the table 'country_stats'
WHERE table_name = 'country_stats';
```