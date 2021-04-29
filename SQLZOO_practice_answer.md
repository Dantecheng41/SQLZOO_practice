# SQLZOO Practice

## SELECT basics

1.  Q : Modify it to show the population of Germany

    A :

```sql
SELECT population
FROM world
WHERE name = 'Germany'
```

2. Q : Show the name and the population for 'Sweden', 'Norway' and 'Denmark'.

   A :

```sql
SELECT name, population
FROM world
WHERE name IN ( 'Sweden', 'Norway' , 'Denmark');
```

3. Q : Modify it to show the country and the area for countries with an area between 200,000 and 250,000.

   A :

```sql
SELECT name, area
FROM world
WHERE area BETWEEN 200000 AND 250000
```

## SELECT basics quiz

1. 3
2. 5
3. 5
4. 3
5. 3
6. 3
7. 3
