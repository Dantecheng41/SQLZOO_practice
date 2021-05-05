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

## SELECT from Nobel Tutorial

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
6. 3
7. 4

## SELECT within SELECT Tutorial

1. Q : List each country name where the population is larger than that of 'Russia'.

   A :

```sql
SELECT name
FROM world
WHERE population >  (SELECT population FROM world  WHERE name='Russia')
```

2. Q : Show the countries in Europe with a per capita GDP greater than 'United Kingdom'.

   A :

```sql
SELECT name
FROM world
WHERE continent = 'Europe' AND gdp/population > (SELECT gdp/population FROM world WHERE name = 'United Kingdom' )
```

3. Q : List the name and continent of countries in the continents containing either Argentina or Australia. Order by name of the country.

   A :

```sql
SELECT name , continent
FROM world
WHERE continent IN (SELECT continent FROM world WHERE name = 'Argentina' OR name = 'Australia') ORDER BY name
```

4. Q : Which country has a population that is more than Canada but less than Poland? Show the name and the population.

   A :

```sql
SELECT name , population
FROM world
WHERE population > (SELECT population FROM world WHERE name = 'Canada') AND population < (SELECT population FROM world WHERE name = 'Poland')
```

5. Q : Show the name and the population of each country in Europe. Show the population as a percentage of the population of Germany.

   A :

```sql
SELECT name, CONCAT(CAST(ROUND(population/(SELECT population FROM world WHERE name = 'Germany')*100, 0) AS INTEGER),'%')
FROM world
WHERE continent = 'Europe'
```

6. Q : Which countries have a GDP greater than every country in Europe? [Give the name only.]

   A :

```sql
SELECT name
FROM world
WHERE gdp > (SELECT MAX(gdp) FROM world WHERE continent = 'Europe')
```

7. Q : Find the largest country (by area) in each continent, show the continent, the name and the area

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

8. Q : List each continent and the name of the country that comes first alphabetically.(p)

   A :

```sql
SELECT continent, name FROM world x
  WHERE name <= ALL
    (SELECT name FROM world y
        WHERE y.continent=x.continent)
```

9. Q : Find the continents where all countries have a population <= 25000000. Then find the names of the countries associated with these continents. Show name, continent and population.

   A :

```sql
SELECT name, continent, CASE WHEN population > 0 THEN population * 3 END
FROM world
WHERE continent = 'Africa'
ORDER BY 3 DESC
```

10. Q : Some countries have populations more than three times that of any of their neighbours (in the same continent). Give the countries and continents.

    A :

```sql
SELECT name,continent
FROM world x
WHERE x.population/3 >= all(select population from world y where x.continent=y.continent and x.name!=y.name and y.population>0)
```

## Nested SELECT Quiz

1. 3
2. 2
3. 1
4. 4
5. 2
6. 2
7. 2

## SUM and COUNT

1. Q : Show the total population of the world.

   A :

```sql
SELECT SUM(population)
FROM world
```

2. Q : List all the continents - just once each.

   A :

```sql
SELECT DISTINCT continent
FROM world
```

3. Q : Give the total GDP of Africa

   A :

```sql
SELECT SUM(gdp)
FROM world
WHERE continent = 'Africa'
```

4. Q : How many countries have an area of at least 1000000

   A :

```sql
SELECT COUNT(DISTINCT name)
FROM world
WHERE area >= 1000000
```

5. Q : What is the total population of ('Estonia', 'Latvia', 'Lithuania')

   A :

```sql
SELECT SUM(population)
FROM world
WHERE name IN ('Estonia', 'Latvia', 'Lithuania')
```

6. Q : For each continent show the continent and number of countries.

   A :

```sql
SELECT continent , COUNT(name)
FROM world
GROUP BY continent
```

7. Q : For each continent show the continent and number of countries with populations of at least 10 million.

   A1 :

```sql
SELECT continent , COUNT(name)
FROM world
WHERE population > 10000000
GROUP BY continent
```

8. Q : List the continents that have a total population of at least 100 million.

   A :

```sql
SELECT continent
FROM world
GROUP BY continent
HAVING SUM(population) > 100000000
```

## SUM and COUNT Quiz

1. 3
2. 1
3. 4
4. 5
5. 2
6. 5
7. 4
8. 4

## The JOIN operation

1. Q : Modify it to show the matchid and player name for all goals scored by Germany. To identify German players, check for: teamid = 'GER'

   A :

```sql
SELECT matchid, player
FROM goal
WHERE teamid = 'GER'
```

2. Q : Show id, stadium, team1, team2 for just game 1012

   A :

```sql
SELECT id,stadium,team1,team2
FROM game
WHERE id = 1012
```

3. Q : Modify it to show the player, teamid, stadium and mdate for every German goal.

   A :

```sql
SELECT player,teamid,stadium,mdate
FROM game JOIN goal ON game.id= goal.matchid
WHERE teamid = 'GER'
```

4. Q : Show the team1, team2 and player for every goal scored by a player called Mario player LIKE 'Mario%'
   A :

```sql
SELECT team1, team2, player
FROM goal JOIN game ON goal.matchid = game.id
WHERE player LIKE 'Mario%'
```

5. Q : Show player, teamid, coach, gtime for all goals scored in the first 10 minutes gtime<=10

   A :

```sql
SELECT player, teamid,coach , gtime
FROM goal JOIN eteam ON teamid = id
WHERE gtime<=10
```

6. Q : List the dates of the matches and the name of the team in which 'Fernando Santos' was the team1 coach.

   A :

```sql
SELECT mdate , teamname
FROM game JOIN eteam ON team1 = eteam.id
WHERE coach = 'Fernando Santos'
```

7. Q : List the player for every goal scored in a game where the stadium was 'National Stadium, Warsaw'

   A :

```sql
SELECT player
FROM goal JOIN game ON matchid=id
WHERE stadium = 'National Stadium, Warsaw'
```

8. Q : Instead show the name of all players who scored a goal against Germany.

   A :

```sql
SELECT DISTINCT player
FROM game JOIN goal ON matchid = id
WHERE (team1='GER' OR team2='GER') AND teamid <> 'GER'
```

9. Q : Show teamname and the total number of goals scored.

   A :

```sql
SELECT teamname, COUNT(gtime)
FROM eteam JOIN goal ON id=teamid
GROUP BY teamname
```

10. Q : Show the stadium and the number of goals scored in each stadium.

    A :

```sql
SELECT stadium, COUNT(gtime)
FROM goal JOIN game ON matchid =id
GROUP BY stadium
```

11. Q : For every match involving 'POL', show the matchid, date and the number of goals scored.

    A :

```sql
SELECT matchid,mdate,COUNT(gtime)
FROM game JOIN goal ON matchid = id
WHERE team1 = 'POL' OR team2 = 'POL'
GROUP BY mdate,matchid
```

12. Q : For every match where 'GER' scored, show matchid, match date and the number of goals scored by 'GER'

    A :

```sql
SELECT matchid,mdate,COUNT(gtime) AS goal
FROM game JOIN goal ON matchid = id
WHERE (team1 = 'GER' OR team2 = 'GER') AND teamid = 'GER'
GROUP BY matchid,mdate
```

13. Q : List every match with the goals scored by each team as shown. This will use "CASE WHEN" which has not been explained in any previous exercises.

    A :

```sql
SELECT mdate, team1, SUM(CASE WHEN teamid=team1 THEN 1 ELSE 0 END) AS score1, team2, SUM(CASE WHEN teamid=team2 THEN 1 ELSE 0 END) AS score2
FROM game JOIN goal ON matchid = id
GROUP BY matchid,mdate,team1,team2
ORDER BY mdate, matchid ,team1 ,team2;
```

## JOIN Quiz

1. 4
2. 3
3. 1
4. 1
5. 2
6. 3
7. 2

## More JOIN operations

1. Q : List the films where the yr is 1962 [Show id, title]

   A :

```sql
SELECT id, title
FROM movie
WHERE yr=1962
```

2. Q : Give year of 'Citizen Kane'.

   A :

```sql
SELECT yr
FROM movie
WHERE title = 'Citizen Kane'
```

3. Q : List all of the Star Trek movies, include the id, title and yr (all of these movies include the words Star Trek in the title). Order results by year.

   A :

```sql
SELECT id, title, yr
FROM movie
WHERE title LIKE 'Star Trek%'
```

4. Q : What id number does the actor 'Glenn Close' have?

   A :

```sql
SELECT id
FROM actor
WHERE name = 'Glenn Close'
```

5. Q : What is the id of the film 'Casablanca'

   A :

```sql
SELECT id
FROM movie
WHERE title = 'Casablanca'
```

6. Q : Obtain the cast list for 'Casablanca'.

   A :

```sql
SELECT name
FROM casting JOIN actor ON id = actorid
WHERE movieid = 27
```

7. Q : Obtain the cast list for the film 'Alien'

   A :

```sql
SELECT name
FROM movie JOIN casting ON movie.id = casting.movieid
JOIN actor ON casting.actorid = actor.id
WHERE title = 'Alien'
```

8. Q : List the films in which 'Harrison Ford' has appeared

   A :

```sql
SELECT title
FROM movie JOIN casting ON movie.id = casting.movieid
JOIN actor ON casting.actorid = actor.id
WHERE name = 'Harrison Ford'
```

9. Q : List the films where 'Harrison Ford' has appeared - but not in the starring role. [Note: the ord field of casting gives the position of the actor. If ord=1 then this actor is in the starring role]

   A :

```sql
SELECT title
FROM movie JOIN casting ON movie.id = casting.movieid
JOIN actor ON casting.actorid = actor.id
WHERE name = 'Harrison Ford' AND ord != 1
```

10. Q : List the films together with the leading star for all 1962 films.

    A :

```sql
SELECT title, name
FROM actor JOIN casting ON actor.id = casting.actorid JOIN movie ON movie.id = casting.movieid
WHERE yr = 1962 AND ord = 1
```

11. Q : Which were the busiest years for 'Rock Hudson', show the year and the number of movies he made each year for any year in which he made more than 2 movies.

    A :

```sql
SELECT yr, COUNT(title)
FROM movie JOIN casting ON movie.id=movieid
JOIN actor ON actorid=actor.id
WHERE name='Rock Hudson'
GROUP BY yr
HAVING COUNT(title) > 1
```

12. Q : List the film title and the leading actor for all of the films 'Julie Andrews' played in.

    A :

```sql
SELECT title, name
FROM actor JOIN casting ON actor.id = casting.actorid
JOIN movie ON movie.id = casting.movieid
WHERE movieid IN (SELECT movieid FROM casting WHERE actorid = (SELECT id FROM actor WHERE name = 'Julie Andrews')) AND ord = 1
ORDER BY title DESC
```

13. Q : Obtain a list, in alphabetical order, of actors who've had at least 15 starring roles.

    A :

```sql
SELECT name
FROM actor JOIN casting ON actor.id = casting.actorid
WHERE ord = 1
GROUP BY name
HAVING COUNT(actorid) >= 15
```

14. Q : List the films released in the year 1978 ordered by the number of actors in the cast, then by title.

    A :

```sql
SELECT DISTINCT title ,COUNT(actorid)
FROM movie JOIN casting ON id = movieid
WHERE yr = 1978
GROUP BY title
ORDER BY COUNT(actorid) DESC ,title
```

15. Q : List all the people who have worked with 'Art Garfunkel'.

    A :

```sql
SELECT DISTINCT name
FROM actor JOIN casting ON actor.id = casting.actorid
JOIN movie ON movie.id = casting.movieid
WHERE actor.id IN ( SELECT actorid FROM casting WHERE movieid IN (SELECT movieid FROM actor JOIN casting ON id = actorid WHERE name = 'Art Garfunkel')) AND name !=  'Art Garfunkel'
```

## JOIN Quiz

1. 3
2. 5
3. 3
4. 2
5. 4
6. 3
7. 2
