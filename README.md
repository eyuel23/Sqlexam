# SQL test Queries

```sql
1,
INSERT INTO Movies (title, runtime, genre, imdb_score, rating)
    -> VALUES ("The Shawshank Redemption", 142, "Drama", 9.3, "R");

2,
SELECT * FROM Movies WHERE genre = 'Sci-Fi';

| id | title             | runtime | genre  | imdb_score | rating |
+----+-------------------+---------+--------+------------+--------+
|  3 | Howard the Duck   |     110 | Sci-fi |        4.6 | PG     |
|  5 | Starship Troppers |     129 | Sci-fi |        7.2 | PG-13

3,
SELECT *
FROM Movies
WHERE imdb_score >= 6.5;

----+--------------------------+---------+-------------+------------+--------+
| id | title                    | runtime | genre       | imdb_score | rating |
+----+--------------------------+---------+-------------+------------+--------+
|  1 | The Shawshank Redemption |     142 | Drama       |        9.3 | R      |
|  2 | The Godfather            |     177 | Crime       |        9.2 | R      |
|  5 | Starship Troppers        |     129 | Sci-fi      |        7.2 | PG-13  |
|  6 | Waltz With Bashir        |      90 | Documentary |        8.0 | R      |
|  7 | Spaceballs               |      96 | Comedy      |        7.1 | PG     |
|  8 | Monsters Inc.            |      92 | Animation   |        8.1 | G

4,
SELECT *
FROM Movies
WHERE (rating = 'G' OR rating = 'PG') AND runtime < 100;

 id | title         | runtime | genre     | imdb_score | rating |
+----+---------------+---------+-----------+------------+--------+
|  7 | Spaceballs    |      96 | Comedy    |        7.1 | PG     |
|  8 | Monsters Inc. |      92 | Animation |        8.1 | G

5,
SELECT genre, AVG(runtime) AS avg_runtime
FROM Movies
WHERE imdb_score < 7.5
GROUP BY genre;

-------+-------------+
| genre  | avg_runtime |
+--------+-------------+
| Sci-fi |    119.5000 |
| Horror |     83.0000 |
| Comedy |     96.0000 |

6,
UPDATE Movies
SET rating = 'R'
WHERE title = 'Starship Troopers';

id | title                    | runtime | genre       | imdb_score | rating |
+----+--------------------------+---------+-------------+------------+--------+
|  1 | The Shawshank Redemption |     142 | Drama       |        9.3 | R      |
|  2 | The Godfather            |     177 | Crime       |        9.2 | R      |
|  3 | Howard the Duck          |     110 | Sci-fi      |        4.6 | PG     |
|  4 | Lavalantula              |      83 | Horror      |        4.7 | TV-14  |
|  5 | Starship Troppers        |     129 | Sci-fi      |        7.2 | PG-13  |
|  6 | Waltz With Bashir        |      90 | Documentary |        8.0 | R      |
|  7 | Spaceballs               |      96 | Comedy      |        7.1 | PG     |
|  8 | Monsters Inc.            |      92 | Animation   |        8.1 | G
Query OK, 1 row affected (0.02 sec)
Rows matched: 1  Changed: 1  Warnings: 0

7,
SELECT id, rating
FROM Movies
WHERE genre IN ('Horror', 'Documentary');

 id | rating |
+----+--------+
|  4 | TV-14  |
|  6 | R      |
+----+--------+
2 rows in set (0.06 sec)

8,
SELECT rating,
       AVG(imdb_score) AS avg_imdb_score,
       MAX(imdb_score) AS max_imdb_score,
       MIN(imdb_score) AS min_imdb_score
FROM Movies
GROUP BY rating;

| rating | avg_imdb_score | max_imdb_score | min_imdb_score |
+--------+----------------+----------------+----------------+
| R      |        8.42500 |            9.3 |            7.2 |
| PG     |        5.85000 |            7.1 |            4.6 |
| TV-14  |        4.70000 |            4.7 |            4.7 |
| G      |        8.10000 |            8.1 |            8.1 |
+--------+----------------+----------------+----------------+
4 rows in set (0.08 sec)


9,
SELECT rating,
       AVG(imdb_score) AS avg_imdb_score,
       MAX(imdb_score) AS max_imdb_score,
       MIN(imdb_score) AS min_imdb_score
FROM Movies
GROUP BY rating
HAVING COUNT(*) > 1;

+--------+----------------+----------------+----------------+
| rating | avg_imdb_score | max_imdb_score | min_imdb_score |
+--------+----------------+----------------+----------------+
| R      |        8.42500 |            9.3 |            7.2 |
| PG     |        5.85000 |            7.1 |            4.6 |
+--------+----------------+----------------+----------------+
2 rows in set (0.09 sec)

10,
DELETE FROM Movies
WHERE rating = 'R';

+----+-----------------+---------+-----------+------------+--------+
| id | title           | runtime | genre     | imdb_score | rating |
+----+-----------------+---------+-----------+------------+--------+
|  3 | Howard the Duck |     110 | Sci-fi    |        4.6 | PG     |
|  4 | Lavalantula     |      83 | Horror    |        4.7 | TV-14  |
|  7 | Spaceballs      |      96 | Comedy    |        7.1 | PG     |
|  8 | Monsters Inc.   |      92 | Animation |        8.1 | G      |
+----+-----------------+---------+-----------+------------+--------+
4 rows in set (0.05 sec

11,
 Drop table Movies;
Query OK, 0 rows affected (0.15 sec)

12,
 DROP DATABASE my_movies;
Query OK, 0 rows affected (0.10 sec)
```
