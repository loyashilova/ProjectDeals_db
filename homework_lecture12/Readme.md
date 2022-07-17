# Домашнее задание по лекции 12

## DML: агрегация и сортировка, CTE, аналитические функции

**Написать запрос суммы очков с группировкой и сортировкой по годам:**

 select year_game, sum(points) as points
 from Statistic
 group by 1 
 
**Написать cte показывающее тоже самое:**

 with sum_points as
 (select year_game, sum(points) as points
 from Statistic
 group by 1
 )
 
select * from sum_points

**Используя функцию LAG вывести кол-во очков по всем игрокам за текущий код и за предыдущий.**

with cte as(

    select player_name, year_game, sum(points) as points
    from Statistic
    group by player_name, year_game
    order by player_name, year_game
)

select player_name, year_game, points, lag(points, 1) over (partition by player_name order by year_game) prv_year_points
from cte