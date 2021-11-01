# Football Matches - Tasks

Each of the questions/tasks below can be answered using a `SELECT` query. When you find a solution copy it into the code block under the question before pushing your solution to GitHub.

1) Find all the matches from 2017.

```sql
<!-- Copy solution here -->

SELECT * FROM matches WHERE season=2017;


----------------------------------------------------------------------


2) Find all the matches featuring Barcelona.

```sql
<!-- Copy solution here -->

SELECT * FROM matches WHERE hometeam='Barcelona' OR awayteam='Barcelona';


----------------------------------------------------------------------


3) What are the names of the Scottish divisions included?

```sql
<!-- Copy solution here -->

SELECT name FROM divisions WHERE country='Scotland';


----------------------------------------------------------------------


4) Find the division code for the Bundesliga. Use that code to find out how many matches Freiburg have played in the Bundesliga since the data started being collected.

```sql
<!-- Copy solution here -->


SELECT code FROM divisions WHERE name='Bundesliga'; 
THEN:
SELECT division_code, COUNT(*) FROM matches WHERE hometeam='Freiburg' OR awayteam='Freiburg' AND division_code='D1' GROUP BY division_code;

----------------------------------------------------------------------


5) Find the unique names of the teams which include the word "City" in their name (as entered in the database)

```sql
<!-- Copy solution here -->

SELECT DISTINCT hometeam FROM matches WHERE hometeam LIKE '%City%';

Either/Or 

SELECT DISTINCT awayteam FROM matches WHERE awayteam LIKE '%City%';


----------------------------------------------------------------------


6) How many different teams have played in matches recorded in a French division?

```sql
<!-- Copy solution here --> TWO SOLUTIONS : both get 61 teams

1) Prints all the team names aswell:

SELECT DISTINCT hometeam FROM matches WHERE division_code='F1' OR division_code='F2' ORDER BY hometeam;

2) Prints just the count;

SELECT COUNT (DISTINCT hometeam) FROM matches WHERE division_code='F1' OR division_code='F2';


COLINS METHOD - MORE STREAMLINED SINCE USES 'IN' FUNCTION (USE WHEN COMPARING MULTIPLE VALUES FROM SAME COLOUMN)

SELECT COUNT (DISTINCT hometeam) FROM matches WHERE division_code IN ('F1', 'F2');

----------------------------------------------------------------------


7) Have Huddersfield played Swansea in the period covered?

```sql
<!-- Copy solution here -->

SELECT COUNT(*) FROM matches WHERE hometeam='Huddersfield' AND awayteam='Swansea' OR  hometeam='Swansea' AND awayteam='Huddersfield';

TO SEE ALL GAME RESULTS BETWEEN THEM- 
-SIMPLY REMOVE COUNT: STILL TELLS NUMBER OF ROWS = NUMBER OF GAMES-

SELECT * FROM matches WHERE hometeam='Huddersfield' AND awayteam='Swansea' OR  hometeam='Swansea' AND awayteam='Huddersfield';

----------------------------------------------------------------------


8) How many draws were there in the Eredivisie between 2010 and 2015?

```sql
<!-- Copy solution here -->


SELECT ftr, COUNT(*) FROM matches WHERE ftr='D' AND division_code='N1' AND 2010<season AND season<2015 GROUP BY ftr;



----------------------------------------------------------------------
Q9) Select the matches played in the Premier League in order of total goals scored from highest to lowest. Where there is a tie the match with more home goals should come first.

```sql
<!-- Copy solution here -->


SELECT * FROM matches WHERE division_code='E0' ORDER BY (fthg+ftag, fthg) DESC;


----------------------------------------------------------------------


10) In which division and which season were the most goals scored?

```sql
<!-- Copy solution here --> 2 PARTER

PART 1) SELECT division_code, season, SUM(fthg + ftag) FROM matches GROUP BY division_code, season ORDER BY SUM DESC LIMIT 1; (this gives division code 'EC' and total goals scored)

PART 2) SELECT name FROM divisions WHERE code='EC';

gives the answer ----> National League

### Useful Resources

- [Filtering results](https://www.w3schools.com/sql/sql_where.asp)
- [Ordering results](https://www.w3schools.com/sql/sql_orderby.asp)
- [Grouping results](https://www.w3schools.com/sql/sql_groupby.asp)
