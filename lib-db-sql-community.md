---
title: lib-db-sql-community
tags: [community, sql]
created: 2023-07-19T10:48:09.951Z
modified: 2023-07-19T10:48:24.003Z
---

# lib-db-sql-community

# guide

# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## This is how SQL get Executed by DB engines
- https://x.com/AmigosCode/status/1841091655786430471

- ✅ Coding Order (How SQL Queries are Written)
1. SELECT: Specifies the columns or expressions to retrieve from the database.
2. FROM: Indicates the table(s) to query and the source of the data.
3. WHERE: Filters the rows based on specified conditions before any grouping or aggregation occurs.
4. GROUP BY: Aggregates rows that share the same values in specified columns into summary rows.
5. HAVING: Filters groups based on a condition, similar to `WHERE` but applied after grouping.
6. ORDER BY: Sorts the result set based on specified columns or expressions.
7. LIMIT: Restricts the number of rows returned by the query.

- ✅ Execution Order (How SQL Queries are Processed)
1. FROM: The query starts by gathering data from the source tables.
2. WHERE: Filters the rows from the `FROM` step based on given conditions.
3. GROUP BY: Organizes filtered rows into groups defined by specified columns.
4. HAVING: Applies conditions to these groups to filter out those that don’t meet the criteria.
5. SELECT: Selects the specific columns or expressions to include in the result set.
6. ORDER BY: Sorts the selected rows according to specified columns.
7. LIMIT: Limits the number of rows returned, based on a specified number.

- ## MySQL perf folks: I have a column that is TEXT, and my queries to find items where that field is null are dog slow (like 30s).
- https://twitter.com/wesbos/status/1737568828022800426
  - How do I speed this up? 
  1. I can't add an index, because there is no length
  2. I can't use varchar because the contents are larger than 16383
- wow lots of good replies! A summary:
  1. Use partial indexes - which wont index the entire text, but will tell  me if it's null quickly [using prisma not supported]
  2. use fulltext index - will index longer text with a bunch of added search features [hit annoying issue]
  3. Add a boolean column + hook on item update. annoying, but fast. 

- Here I am! If you only need to check for null/not null, you could add a functional index on that expression. Then you don't have to maintain a second column or change your queries. You can even add that as a part of a compound index, to make it more selective.
  - looks like Prisma doesn't support it - gonna go with the boolean approach
- If Prisma supports generated columns you could do that as well. That way you don't have to maintain state, the database will do it

- You can use a generated column that is stored. It will auto update itself anytime you change the text column.

- ## TIL: In SQL, looking for "all rows without a specific value" will not include rows containing NULL 
- https://twitter.com/damienalexandre/status/1732391868132913226
  - That's really unexpected behavior on all engines: #mysql, #postgresql...

- The SQL Standard clearly states that 
  1. that the WHERE clause returns all rows for which its predicate evaluates to TRUE. 
  2. that any comparison with NULL evaluates to UNKNOWN, and
  3. that UNKNOWN and TRUE are not the same thing.

- So do you need to use `val != 'crazy' OR val IS NULL` ?
  - Yes, absolutely
- What about NOT IN?
  - Same behavior
- PostgreSQL offers IS DISTINCT FROM

- ## When you are writing SQL queries, remember that the precedence of `OR` operator is different from `AND` operator, just as most programming languages do. 
- https://twitter.com/leiysky/status/1681597163946807296
  - Care of it, or you will be suffered
