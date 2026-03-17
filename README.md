#  # Домашнее задание к занятию "SQL" - Марчук Кирилл



### Задание 1 Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию:
фамилия и имя сотрудника из этого магазина;
город нахождения магазина;
количество пользователей, закреплённых в этом магазине.


1. `Создаём запрос в mysql`


```

SELECT 
    CONCAT(s.first_name, ' ', s.last_name) AS employee_name,
    ci.city AS store_city,
    COUNT(c.customer_id) AS customer_count
FROM store st
JOIN staff s ON st.manager_staff_id = s.staff_id
JOIN address a ON st.address_id = a.address_id
JOIN city ci ON a.city_id = ci.city_id
JOIN customer c ON st.store_id = c.store_id
GROUP BY st.store_id, employee_name, store_city
HAVING customer_count > 300;

```


---

### Задание 2 Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.



1. `Проверим, сколько фильмов загрузилось`
2. `Проверим среднюю продолжительность`
3. `Выполним запрос на продолжительность которых больше средней продолжительности всех фильмов`



```

#Сколько фильмов загрузилось
SELECT COUNT(*) AS total_films FROM film;

#Cредняя продолжительность
SELECT AVG(length) AS average_length FROM film;

#Продолжительность больше средней продолжительности
SELECT COUNT(*) AS films_longer_than_average
FROM film
WHERE length > (SELECT AVG(length) FROM film);

```

![zadanie2](https://github.com/ottofonciceron-coder/SQL-12-04-hw/blob/main/zadanie%202.png)`


---

### Задание 3 Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.


1. `Выполняем запрос в mysql`


```

SELECT 
    DATE_FORMAT(payment_date, '%Y-%m') AS month_with_year,
    DATE_FORMAT(payment_date, '%M %Y') AS full_month_name,
    SUM(amount) AS total_payments,
    COUNT(DISTINCT rental_id) AS rental_count
FROM payment
GROUP BY month_with_year, full_month_name
ORDER BY total_payments DESC
LIMIT 1;

```

![zadanie3](https://github.com/ottofonciceron-coder/SQL-12-04-hw/blob/main/Zadanie%203.png)`

1. `Самый прибыльный месяц Июль 2005 года`
2. `Общая сумма платежей: $28,368.91`
3. `Количество аренд: 6,709 и кол-во платежей: 6,709`
4. `Средний платеж: $4.23`

---

