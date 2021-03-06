# Codecademy SQL Project

[Twitch](https://www.twitch.tv) is the world’s leading video platform and community for gamers, with more than 15+ million unique daily visitors. In this project, you will be working with two fictional tables that contain Twitch's streaming data and chat room data and answering questions about them:

- Streaming data is in the `stream` table
- Chat usage data is in the `chat` table

Each question can be answered using one (or more) SQL queries. The answer to the first question is given. The rest is for you to figure out. Let's get started!

---

1. `SELECT` all columns from the first 20 rows of `stream` table.

```sql
SELECT *
FROM stream
LIMIT 20;
```

2. `SELECT` all columns from the first 20 rows of `chat` table.

```sql
SELECT *
FROM chat
LIMIT 20;
```


3. There is something wrong with the `chat` table. Its 1st row is actually the column names. Delete the first row of the `chat` table.

```sql
DELETE FROM chat
WHERE time = 'time';
```

4. What are the `DISTINCT` `game` in the `stream` table?

```sql
SELECT DISTINCT game
FROM stream;
```

5. What are the `DISTINCT` `channel`s in the `stream` table?

```sql
SELECT DISTINCT channel
FROM stream;
```

6. What are the most popular games in `stream`? Create a list of games and their number of viewers. `ORDER BY` from most popular to least popular.

```sql
SELECT game, COUNT (login)
FROM stream
GROUP BY game
ORDER BY count(login) DESC;
```

7. There are some big numbers from the game `League of Legends` in `stream`. Where are these `League of Legend players` located? 

    - **Hint:** Create a list.
	
```sql
SELECT DISTINCT country FROM stream
    WHERE game = 'League of Legends';
```

8. The `player` column shows the source/device the viewer is using (site, iphone, android, etc). Create a list of players and their number of streamers.

```sql
SELECT player, COUNT (login)
FROM stream
GROUP BY player
ORDER BY count(login) DESC;
```

9. Using a `CASE` statement, create a new column named `genre` for each of the games in `stream`. Group the games into their genres: Multiplayer Online Battle Arena (MOBA), First Person Shooter (FPS), and Others. Your logic should be: *If it is `League of Leagues` or `Dota 2` or `Heroes of the Storm` → then it is `MOBA`. If it is `Counter-Strike: Global Offensive` → then it is `FPS`. Else, it is `Others`.* 

    - **Hint:** Use `GROUP BY` and `ORDER BY` to showcase only the unique game titles.

```sql	
SELECT *,
    CASE 
    WHEN game = 'League of Legends' OR game = 'Dota 2' OR game = 'Heroes of the Storm' THEN 'MOBA'
    WHEN game = 'Counter-Strike: Global Offensive' THEN 'FPS'
    ELSE 'Others'
    END as 'genre'
FROM stream
-- Remove the next two lines to return to the full table. 
GROUP BY game
ORDER BY genre;
```

10. The `stream` table and the `chat` table share a column: `device_id`. Do a `JOIN` of the two tables on that column.

```sql
SELECT *
FROM stream
JOIN chat
    ON stream.device_id = chat.device_id;
```
	
---

**Bonus:** Now try to find some other interesting insights from these two tables using SQL!

```sql
-- Shows the breakdown of people watching based on the hour
SELECT SUBSTR(time, 12, 2) AS 'hour', COUNT(Login)
FROM stream
GROUP BY hour;
```

```sql
-- This breaks down each channel by the number of viewers per game, changing to chat can show the variance between chat views and stream views
SELECT channel, game, COUNT (login)
FROM stream
GROUP BY channel, game
ORDER BY channel, count(login) DESC;
```

