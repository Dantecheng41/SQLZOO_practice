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

## SELECT from WORLD Tutorial

1.  Q : Observe the result of running this SQL command to show the name, continent and population of all countries.

    A :

```sql
SELECT name, continent, population
FROM world
```

2.  Q : Show the name for the countries that have a population of at least 200 million. 200 million is 200000000, there are eight zeros.

    A :

```sql
SELECT name
FROM world
WHERE population >= 200000000
```

3.  Q : Give the name and the per capita GDP for those countries with a population of at least 200 million.

    A :

```sql
SELECT name , gdp/population
FROM world
WHERE population >= 200000000
```

4.  Q : Show the name and population in millions for the countries of the continent 'South America'. Divide the population by 1000000 to get population in millions.

    A :

```sql
SELECT name , population/1000000
FROM world
WHERE continent = 'South America'
```

5.  Q : Show the name and population for France, Germany, Italy

    A :

```sql
SELECT name , population
FROM world
WHERE name IN ('France', 'Germany', 'Italy')
```

6.  Q : Show the countries which have a name that includes the word 'United'

    A :

```sql
SELECT name
FROM world
WHERE name LIKE '%United%'
```

7.  Q : Two ways to be big: A country is big if it has an area of more than 3 million sq km or it has a population of more than 250 million.
    Show the countries that are big by area or big by population. Show name, population and area.

    A :

```sql
SELECT name , population , area
FROM world
WHERE area > 3000000 OR population > 250000000
```

8.  Q : Exclusive OR (XOR). Show the countries that are big by area (more than 3 million) or big by population (more than 250 million) but not both. Show name, population and area.

    A :

```sql
SELECT name , population , area
FROM world
WHERE area > 3000000 AND population < 250000000 OR area < 3000000 AND population > 250000000
```

9.  Q : Show the name and population in millions and the GDP in billions for the countries of the continent 'South America'. Use the ROUND function to show the values to two decimal places.

    A :

```sql
SELECT name, ROUND(population/1000000,2), ROUND(gdp/1000000000,2)
FROM world
WHERE continent = 'South America'
```

10. Q : Show the name and per-capita GDP for those countries with a GDP of at least one trillion (1000000000000; that is 12 zeros). Round this value to the nearest 1000.

    A :

```sql
SELECT name , ROUND(gdp/population,-3)
FROM world
WHERE gdp >= 1000000000000
```

11. Q : Show the name and capital where the name and the capital have the same number of characters.

    A :

```sql
SELECT name, capital
FROM world
WHERE LEN(name) = LEN(capital)
```

12. Q : Show the name and the capital where the first letters of each match. Don't include countries where the name and the capital are the same word.

    A :

```sql
SELECT name, capital
FROM world
WHERE LEFT(name,1) = LEFT(capital,1) and name <> capital
```

13. Q : Equatorial Guinea and Dominican Republic have all of the vowels (a e i o u) in the name. They don't count because they have more than one word in the name.
    Find the country that has all the vowels and no spaces in its name.

    A :

```sql
SELECT name
FROM world
WHERE name NOT LIKE '% %' AND name LIKE '%a%' AND name LIKE '%e%' AND name LIKE '%i%' AND name LIKE '%o%' AND name LIKE '%u%'
```

## BBC QUIZ

1. 5
2. 4
3. 2
4. 4
5. 2
6. 4
7. 3

## SELECT from WORLD Tutorial

1. Q : Change the query shown so that it displays Nobel prizes for 1950.

   A :

```sql
SELECT yr, subject, winner
FROM nobel
WHERE yr = 1950
```

2. Q : Show who won the 1962 prize for Literature.

   A :

```sql
SELECT winner
FROM nobel
WHERE yr = 1962 AND subject = 'Literature'
```

3. Q : Show the year and subject that won 'Albert Einstein' his prize.

   A :

```sql
SELECT yr, subject
FROM nobel
WHERE winner = 'Albert Einstein'
```

4. Q : Give the name of the 'Peace' winners since the year 2000, including 2000.
   A :

```sql
SELECT winner
FROM nobel
WHERE yr >= 2000 AND subject = 'Peace'
```

5. Q : Show all details (yr, subject, winner) of the Literature prize winners for 1980 to 1989 inclusive.

   A :

```sql
SELECT yr , subject ,winner FROM nobel
WHERE subject = 'Literature' AND yr BETWEEN 1980 AND 1989
```

6. Q : Show all details of the presidential winners:
   Theodore Roosevelt
   Woodrow Wilson
   Jimmy Carter
   Barack Obama

   A :

```sql
SELECT *
FROM nobel
WHERE winner IN ('Theodore Roosevelt','Woodrow Wilson','Jimmy Carter','Barack Obama')
```

7. Q : Show the winners with first name John

   A :

```sql
SELECT winner
FROM nobel
WHERE winner LIKE 'John%'
```

8. Q : Show the year, subject, and name of Physics winners for 1980 together with the Chemistry winners for 1984.

   A :

```sql
SELECT *
FROM nobel
WHERE (subject = 'Physics' AND yr = 1980) OR (subject = 'Chemistry' AND yr = 1984)
```

9. Q : Show the year, subject, and name of winners for 1980 excluding Chemistry and Medicine

   A :

```sql
SELECT *
FROM  nobel
WHERE yr = 1980 AND subject NOT IN ('Chemistry' , 'Medicine')
```

10. Q : Show year, subject, and name of people who won a 'Medicine' prize in an early year (before 1910, not including 1910) together with winners of a 'Literature' prize in a later
    year(after 2004, including 2004)

    A :

```sql
SELECT *
FROM nobel
WHERE subject = 'Medicine' AND yr < 1910 OR subject = 'Literature' AND yr >= 2004
```

11. Q : Find all details of the prize won by PETER GRÜNBERG

    A :

```sql
SELECT *
FROM nobel
WHERE winner = 'PETER GRÜNBERG'
```

12. Q : Find all details of the prize won by EUGENE O'NEILL

    A :

```sql
SELECT *
FROM nobel
WHERE winner = 'EUGENE O''NEILL'
```

13. Q : List the winners, year and subject where the winner starts with Sir. Show the the most recent first, then by name order.

    A :

```sql
SELECT winner, yr, subject
FROM nobel
WHERE winner LIKE 'SIR%' ORDER BY yr DESC , winner
```

14. Q : Show the 1984 winners and subject ordered by subject and winner name; but list Chemistry and Physics last.

    A :

```sql
SELECT winner, subject
FROM nobel
WHERE yr=1984 ORDER BY CASE WHEN subject IN ('Chemistry', 'Physics') THEN 1 ELSE 0 END, subject, winner
```

## BBC QUIZ

1. 5
2. 3
3. 2
4. 3
5. 3
6. 4
7. 3

## SELECT within SELECT Tutorial

1.  Q : Find the largest country (by area) in each continent, show the continent, the name and the area

    A1 :

```sql
SELECT continent, name, area
FROM world x
WHERE area >= ALL(SELECT area
                  FROM world y
                  WHERE y.continent=x.continent AND area>0)
```

    A2 :

```sql
SELECT x.continent, x.name, x.area
FROM world x
JOIN  (SELECT continent, MAX(area) AS area FROM world GROUP BY continent) AS y ON y.continent=x.continent
WHERE x.area >= y.area
```
