# **Домашнее задание к занятию "Индексы"**-***Вуколов Евгений***


## **Задание 1**

- ![scrinshot](https://github.com/Evgenii-379/12-05.md/blob/main/Снимок%20экрана%202024-05-28%20212524.png)

Убрал таблицу inventory

## **Задание 2**

В запросе есть узкие места, которые выражаются более увеличенным временем:

Table scan on <temporary>  (cost=2.5..2.5 rows=0) (actual time=4264..4264 rows=391 loops=1)
- Temporary table with deduplication  (cost=0..0 rows=0) (actual time=4264..4264 rows=391 loops=1)
-   Window aggregate with buffering: sum(payment.amount) OVER (PARTITION BY c.customer_id,f.title )   (actual time=1943..4121 rows=642000 loops=1)
-      Sort: c.customer_id, f.title  (actual time=1943..1984 rows=642000 loops=1)
-         Stream results  (cost=17.1e+6 rows=16.3e+6) (actual time=2.2..1290 rows=642000 loops=1)
-            Nested loop inner join  (cost=17.1e+6 rows=16.3e+6) (actual time=2.19..1106 rows=642000 loops=1)
-                Nested loop inner join  (cost=15.4e+6 rows=16.3e+6) (actual time=2.18..977 rows=642000 loops=1)
-                   Nested loop inner join  (cost=13.8e+6 rows=16.3e+6) (actual time=2.16..845 rows=642000 loops=1)


-  Covering index lookup on r using rental_date (rental_date=p.payment_date)  (cost=0.656 rows=1.01) (actual time=820e-6..0.00116 rows=1.01 loops=634000)
-    Single-row index lookup on c using PRIMARY (customer_id=r.customer_id)  (cost=250e-6 rows=1) (actual time=95.3e-6..110e-6 rows=1 loops=642000)
-      Single-row covering index lookup on i using PRIMARY (inventory_id=r.inventory_id)  (cost=250e-6 rows=1) (actual time=82.2e-6..98.4e-6 rows=1 loops=642000)
 

- ![scrinshot](https://github.com/Evgenii-379/12-05.md/blob/main/Снимок%20экрана%202024-05-29%20233238.png)
- ![scrinshot](https://github.com/Evgenii-379/12-05.md/blob/main/Снимок%20экрана%202024-05-29%20231737.png)
- ![scrinshot](https://github.com/Evgenii-379/12-05.md/blob/main/Снимок%20экрана%202024-05-29%20213315.png)

Добавил индекс в таблицу payment: fk_payment_date
Таблица payment: индекс - fk_amount
Таблица customer: индекс - idx_first_name
Убрал таблицу inventory
При добавлении индексов время запроса уменьшилось с 3,52 секунд до 3,42


 
