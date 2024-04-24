
DAY 3
# SQL Lesson 1: SELECT queries 101

1. Find the title of each film ✓

` SELECT title FROM movies; `

2. Find the director of each film ✓

` SELECT director FROM movies; `



3. Find the title and director of each film ✓

` SELECT Title, director FROM movies; `

4. Find the title and year of each film ✓

` SELECT Title, year FROM movies; `

5. Find all the information about each film ✓

` SELECT * from Movies; `



# SQL Lesson 2: Queries with constraints (Pt. 1)

- conditions: between...and..,in,not in, 

- inclusive for 1.5 and 10.5( 10.5 is included)



1.Find the movie with a row id of 6

` SELECT * FROM movies where id = 6; `

2.Find the movies released in the years between 2000 and 2010

` SELECT * FROM movies where year between 2000 and 2010; `

3.Find the movies not released in the years between 2000 and 2010

` SELECT * FROM movies where year not between 2000 and 2010; `

4.Find the first 5 Pixar movies and their release year

` SELECT * FROM movies where id<=5; `

### for In

select * from movies where year in(1999,2000,2010);

# SQL Lesson 3: Queries with constraints (Pt. 2)

- = exactly matches the kw
- like is case insensi

- operators
  ```
  - name = "abc" ( matches only the pattern)
  - name LIKE "abc" (case insensitive)
  - name LIKE "%AT%" (matches word with these letters including AT)
  - name like "AN_" (matches with another one letter after AN)
  ```


1. Find all the Toy Story movies ✓

  ` SELECT * FROM movies where title like "Toy Story%"; `

2. Find all the movies directed by John Lasseter ✓


` SELECT * FROM movies where Director="John Lasseter"; `


3. Find all the movies (and director) not directed by John Lasseter ✓

` SELECT * FROM movies  where not Director = "John Lasseter" `
;

4. Find all the WALL-* movies ✓

` SELECT * FROM movies where title like "wall-%"; `

-- comment line in sql

# SQL Lesson 4: Filtering and sorting Query results

- to remove duplicate rows

```
SELECT DISTINCT column, another_column, …
FROM mytable
WHERE condition(s);
```

- order by by default it is asc

- limit 5 - gives top 5

- limit 2 offset 2 (first 2 skipped then 2 displayed)

- SYntax for limit and offset:
```
SELECT column, another_column, …
FROM mytable
WHERE condition(s)
ORDER BY column ASC/DESC
LIMIT num_limit OFFSET num_offset;
```


1. List all directors of Pixar movies (alphabetically), without duplicates ✓


>SELECT distinct director FROM movies order by Director asc; 


2.List the last four Pixar movies released (ordered from most recent to least)


>SELECT * FROM movies order by Year desc limit 4; 


3. List the first five Pixar movies sorted alphabetically

>SELECT * FROM movies order by title asc limit 5; 


4. List the next five Pixar movies sorted alphabetically


> SELECT * FROM movies order by title asc limit 5 offset 5; 


# SQL Review: Simple SELECT Queries


1. List all the Canadian cities and their populations ✓


` SELECT * FROM north_american_cities where country = "Canada";`

2. Order all the cities in the United States by their latitude from north to south ✓

`SELECT * FROM north_american_cities where country = "United States" order by latitude desc; `

3. List all the cities west of Chicago, ordered from west to east ✓

```
SELECT * FROM north_american_cities
where longitude < -87.629798
order by longitude ;
```

4. List the two largest cities in Mexico (by population) ✓

```
SELECT * FROM north_american_cities
where country = "Mexico"
order by population desc
limit 2;
```

5. List the third and fourth largest cities (by population) in the United States and their population ✓

```
SELECT * FROM north_american_cities
where country = "United States"
order by population desc
limit 2 offset 2;
```

# SQL Lesson 6: Multi-table queries with JOINs 😢


## INNER JOIN

### sytanx:

```
SELECT column, another_table_column, …
FROM mytable
INNER JOIN another_table 
    ON mytable.id = another_table.id
WHERE condition(s)
ORDER BY column, … ASC/DESC
LIMIT num_limit OFFSET num_offset;
```

1. Find the domestic and international sales for each movie ✓

```
SELECT title, domestic_sales, international_sales from Movies
inner join Boxoffice
on id = movie_id;
```

2. Show the sales numbers for each movie that did better internationally rather than domestically ✓

```
SELECT title, domestic_sales, international_sales from Movies
inner join Boxoffice
on id = movie_id
where international_sales > domestic_sales;
```

3. List all the movies by their ratings in descending order ✓

```
SELECT title, domestic_sales, international_sales from Movies
inner join Boxoffice
on id = movie_id
order by rating desc;
```

## left, right, outer joins

```
SELECT column, another_column, …
FROM mytable
INNER/LEFT/RIGHT/FULL JOIN another_table 
    ON mytable.id = another_table.matching_id
WHERE condition(s)
ORDER BY column, … ASC/DESC
LIMIT num_limit OFFSET num_offset;
```

1. Find the list of all buildings that have employees ✓

> SELECT distinct building FROM employees;



2. Find the list of all buildings and their capacity ✓

>SELECT * FROM Buildings;

3. List all buildings and the distinct employee roles in each building (including empty buildings) ✓

```
SELECT DISTINCT building_name, role 
FROM buildings 
  LEFT JOIN employees
    ON building_name = building;
```

# SQL Lesson 8: A short note on NULLs

### syntax:

```
 SELECT column, another_column, …
FROM mytable
WHERE column IS/IS NOT NULL
AND/OR another_condition
AND/OR …;
```

1. Find the name and role of all employees who have not been assigned to a building ✓

> SELECT name, role 
 FROM employees
 where building is null;

2. Find the names of the buildings that hold no employees

> SELECT building_name
FROM buildings
left join employees on building_name = building
where building is null
;

# SQL Lesson 9: Queries with expressions

