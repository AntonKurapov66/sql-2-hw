# Домашнее задание к занятию "SQL. Часть 1" - `Курапов Антон`


### Задание 1
* Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию:
   * фамилия и имя сотрудника из этого магазина;
   * город нахождения магазина;
   * количество пользователей, закреплённых в этом магазине.
     
 ![alt text](https://github.com/AntonKurapov66/sql_1_hw/blob/main/img/1.PNG)
```sql
	select
	st.last_name 'Фамилия', st.first_name 'Имя', ci.city 'Город',count(cu.customer_id) 'Кол-во клиентов'
	from customer cu
	join staff st on (st.store_id = cu.store_id )
	join address ad on (ad.address_id = st.address_id)
	join city ci on (ci.city_id = ad.city_id)
	group by st.first_name , st.last_name , ci.city
	having count(cu.customer_id)>300;
```
### Задание 2
* Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.
  
 ![alt text](https://github.com/AntonKurapov66/sql_1_hw/blob/main/img/1.PNG)
```sql
	select count(film_id) from film f
	where `length` > (select avg(`length`) from film f2);
```
### Задание 3
* Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.

 ![alt text](https://github.com/AntonKurapov66/sql_1_hw/blob/main/img/1.PNG)
```sql
	select 
	date_format(p.payment_date,'%M-%Y') 'Месяц-Год', sum(p.amount) 'Сумма платежей', count(r.rental_id) 'Кол-во аренд' 
	from payment p 
	join rental r on (p.rental_id = r.rental_id)
	group by date_format(payment_date,'%M-%Y')
	order by sum(p.amount) desc
	limit 1;
```
### Задание 4*
* Посчитайте количество продаж, выполненных каждым продавцом. Добавьте вычисляемую колонку «Премия». Если количество продаж превышает 8000, то значение в колонке будет «Да», иначе должно быть значение «Нет».

 ![alt text](https://github.com/AntonKurapov66/sql_1_hw/blob/main/img/1.PNG)
```sql
	select staff_id 'Менеджер', count(payment_id) 'Кол-во продаж',
		case 
			when count(payment_id) > 8000 then 'ДА'
			else 'НЕТ'
		end as 'Премия'
	from payment p 
	group by staff_id; 
```
 

