# MySQL

---

## Типы данных

**Символьные типы**

| Тип | Описание |
| --- | -------- |
| `CHAR` | Строка фиксированной длины. Длина хранимой строки указыватся в скобках, например, CHAR(10) - строка из десяти символов. И если в таблицу в данный столбец сохраняется строка из 6 символов (то есть меньше установленной длины в 10 символов), то строка дополняется 4 пробелами и в итоге все равно будет занимать 10 символов. Тип CHAR может хранить до 255 байт. |
| `VARCHAR` | Строка переменной длины. Длина хранимой строки также указыватся в скобках, например, VARCHAR(10). Однако в отличие от CHAR хранимая строка будет занимать именно столько места, скольо необходимо. Например, если определеная длина в 10 символов, но в столбец сохраняется строка в 6 символов, то хранимая строка так и будет занимать 6 символов плюс дополнительный байт, который хранит длину строки. Всего тип VARCHAR может хранить до 65535 байт. |
| `TINYTEXT` | Текст длиной до 255 байт. |
| `TEXT` | Текст длиной до 65 КБ. |
| `MEDIUMTEXT` | Текст длиной до 16 МБ |
| `LARGETEXT` | Текст длиной до 4 ГБ |

*Начиная с MySQL 5.6 типы CHAR и VARCHAR по умолчанию используют кодировку UTF-8, которая позволяет использовать до 3 байт для хранения символа в заивисимости от языка ( для многих европейских языков по 1 байту на символ, для ряда восточно-европейских и ближневосточных - 2 байта, а для китайского, яполнского, корейского - по 3 байта на символ).*

**Числовые типы**

| Тип | Описание |
| --- | -------- |
| `TINYINT` | Целые числа от -128 до 127, занимает 1 байт |
| `BOOL` | Фактически не представляет отдельный тип, а является лишь псевдонимом для типа TINYINT(1) и может хранить два значения 0 и 1. Однако данный тип может также в качестве значения принимать встроенные константы TRUE (представляет число 1) и FALSE (предоставляет число 0). Также имеет псевдоним BOOLEAN. |
| `TINYINT UNSIGNED` | Целые числа от 0 до 255, занимает 1 байт |
| `SMALLINT` | Целые числа от -32768 до 32767, занимает 2 байтa |
| `SMALLINT UNSIGNED` | Целые числа от 0 до 65535, занимает 2 байтa |
| `MEDIUMINT` | Целые числа от -8388608 до 8388607, занимает 3 байта |
| `MEDIUMINT UNSIGNED` | Целые числа от 0 до 16777215, занимает 3 байта |
| `INT` | Целые числа от -2147483648 до 2147483647, занимает 4 байта |
| `INT UNSIGNED` | Целые числа от 0 до 4294967295, занимает 4 байта |
| `BIGINT` | Целые числа от -9 223 372 036 854 775 808 до 9 223 372 036 854 775 807, занимает 8 байт |
| `BIGINT UNSIGNED` | Целые числа от 0 до 18 446 744 073 709 551 615, занимает 8 байт |
| `DECIMAL` | Хранит числа с фиксированной точностью. Данный тип может принимать два параметра precision и scale: DECIMAL(precision, scale). |
| `FLOAT` | Хранит дробные числа с плавающей точкой одинарной точности от -3.4028 * 1038 до 3.4028 * 1038, занимает 4 байта |
| `DOUBLE` | Хранит дробные числа с плавающей точкой двойной точности от -1.7976 * 10308 до 1.7976 * 10308, занимает 8 байт. Также может принимать форму DOUBLE(M,D), где M - общее количество цифр, а D - количество цифр после запятой. |

**Дата и время**

| Тип | Описание |
| --- | -------- |
| `DATE` | Хранит даты с 1 января 1000 года до 31 деабря 9999 года (c "1000-01-01" до "9999-12-31"). По умолчанию для хранения используется формат yyyy-mm-dd. Занимает 3 байта. |
| `TIME` | Хранит время от -838:59:59 до 838:59:59. По умолчанию для хранения времени применяется формат "hh:mm:ss". Занимает 3 байта. |
| `DATETIME` | Объединяет время и дату, диапазон дат и времени - с 1 января 1000 года по 31 декабря 9999 года (с "1000-01-01 00:00:00" до "9999-12-31 23:59:59"). Для хранения по умолчанию используется формат "yyyy-mm-dd hh:mm:ss". Занимает 8 байт |
| `TIMESTAMP` | Также хранит дату и время, но в другом диапазоне: от "1970-01-01 00:00:01" UTC до "2038-01-19 03:14:07" UTC. Занимает 4 байта |
| `YEAR` | Хранит год в виде 4 цифр. Диапазон доступных значений от 1901 до 2155. Занимает 1 байт. |

Тип Date может принимать даты в различных форматах, однако непосредственно для хранения в самой бд даты приводятся к формату "yyyy-mm-dd". Некоторые из принимаемых форматов:
- yyyy-mm-dd - 2018-05-25 
- yyyy-m-dd - 2018-5-25 
- yy-m-dd - 18-05-25

В таком формате двузначные числа от 00 до 69 воспринимаются как даты в диапазоне 2000-2069. А числа от 70 до 99 как диапазон чисел 1970 - 1999.
- yyyymmdd - 20180525 
- yyyy.mm.dd - 2018.05.25

Для времени тип Time использует 24-часовой формат. Он может принимать время в различных форматах:
- hh:mi - 3:21 (хранимое значение 03:21:00)
- hh:mi:ss - 19:21:34 
- hhmiss - 192134

Примеры значений для типов DATETIME и TIMESTAMP:
- 2018-05-25 19:21:34 
- 2018-05-25 (хранимое значение 2018-05-25 00:00:00)

**Составные типы**

| Тип | Описание |
| --- | -------- |
| `ENUM` | Хранит одно значение из списка допустимых значений. Занимает 1-2 байта |
| `SET` | Может хранить несколько значений (до 64 значений) из некоторого списка допустимых значений. Занимает 1-8 байт. |

**Бинарные типы**

| Тип | Описание |
| --- | -------- |
| `TINYBLOB` | Хранит бинарные данные в виде строки длиной до 255 байт. |
| `BLOB` | Хранит бинарные данные в виде строки длиной до 65 КБ. |
| `MEDIUMBLOB` | Хранит бинарные данные в виде строки длиной до 16 МБ |
| `LARGEBLOB` | Хранит бинарные данные в виде строки длиной до 4 ГБ |

---

#### Основные команды

| Команда                                                                              | Описание                                       |
|--------------------------------------------------------------------------------------|------------------------------------------------|
| `mysql -u root -p`                                                                   | Авторизация под пользователем root             |
| `mysql.server start`                                                                 | Start mysql на macos                           |
| `sudo service mysql start/restart/stop`                                              | Старт, рестарт, стоп mysql в Ubuntu            |
| `mysqldump -uroot -p db_name > file_name.sql`                                        | Бэкап базы данных                              |
| `mysql db_name -u user_name -p < dump.sql`                                           | Залить базу на сервер mysql                    |
| `show databases`                                                                     | Показать список всех баз данных                |
| `use db_name`                                                                        | Переход в определенную базу данных             |
| `show tables`                                                                        | Показать все таблицы в базе данных             |
| `show columns from table_name`                                                       | Показать все столбцы в таблице                 |
| `show index from persons`                                                            | Отобразить индексы для таблицы                 |
| `create index index_name on tb_name (column_name)`                                   | Создание простого индекса для ускорения поиска |
| `drop index index_name on tb_name` | Удаление индекса                               |
| `alter table orders drop foreign key fk_client_id` | Удаление внешнего ключа                        |
| `select count(*) from table_name`                                                    | Считаем количество записей в таблице           |
| `select count(distinct user_id) from balance_log`                                    | Подсчет уникальных значений в столбце          |
| `truncate table tb_name`                                                             | Очистить таблицу                               |
| `alter table table_name convert to character set utf8mb4 collate utf8mb4_unicode_ci` | Изменение кодировки таблицы                    |
| `git reset --keep HEAD@{1}`                                                          | Сброс последнего pull                          |

#### CREATE

| Команда | Описание |
| ------------- | ------------- |
| `create database db_name` | Создание базы данных |
| `create user 'userName'@'localhost' identified by 'password'` | Создание пользователя БД |

##### Создание таблицы

```mysql
CREATE TABLE persons
(
    id  int not null auto_increment primary key,
    last_name  varchar(255),
    first_name varchar(255),
    phone   varchar(255)
);
```

#### INSERT

##### Вставка записи с рандомными значениями

```mysql
insert into persons (last_name, first_name, phone)
values(LEFT(UUID(), 15), LEFT(UUID(), 16), concat(799912345, FLOOR(RAND()*(25-10+1))+10))
```

##### Вставка рандомных записей с удвоением

*Запрос выбирает все записи из бд и добавляет столько же новых*

```mysql
INSERT INTO persons (last_name, first_name, phone)
SELECT concat(left(last_name, 30), uuid()), concat(left(first_name, 29), uuid()), concat(799912345, FLOOR(RAND()*(25-10+1))+10)
FROM   persons
WHERE  id > 1
```

#### UPDATE

| Команда | Описание |
| ------------- | ------------- |
| `update ips set tm_last_seen='2022-05-23 18:08:58'` | Обновить таблицу ips, установить всем значениям в столбце `tm_last_seen` = дате |
| `update users set users.email = users.id` | Присвоить значение столбца `id` столбцу `email` в таблице `users` |

#### DROP

| Команда | Описание |
| ------------- | ------------- |
| `drop user 'userName'@'localhost'` | Удаление пользователя БД |
| `drop table persons` | Удаление таблицы |

#### FOREIGN KEY

*Содание внешнего ключа (две таблицы: orders, clients)*

```mysql
alter table mysql_study_db_1.orders add constraint fk_client_id foreign key (client_id) references mysql_study_db_1.clients(id) on delete cascade
```

#### SELECT

| Команда | Описание |
| ------------- | ------------- |
| `select * from users` | Показать все записи из таблицы users |
| `select * from users where balance = 10` | Показать все записи из таблицы users, где balance = 10 |
| `select * from users where balance = 10 and mfa = 0` | Показать все записи из таблицы users, где balance = 10 и mfa = 0 |

#### GRANT

| Команда | Описание |
| ------- | -------- |
| `GRANT ALL PRIVILEGES ON db_name.* TO user@localhost with grant option;` | Даем привилегии на базу данных определенному пользователю |

#### UNION

| Команда | Описание |
| ------- | -------- |
| `select sum(sum) as salary_log from user_salary_log where user_id = 30955 UNION select salary as salary from users where id = 30955` | Объединение двух запросов в один |

#### SETTING

| Команда | Описание |
| ------- | -------- |
| `show variables like 'lower_case_%'` | Показывает состояние вкл/выкл приведения к нижнему регистру |

**ERROR 1819 (HY000): Your password does not satisfy the current policy requirements**

**Фикс:**  
- выполняем: `SHOW VARIABLES LIKE 'validate_password%';`  
```
+--------------------------------------+--------+
| Variable_name                        | Value  |
+--------------------------------------+--------+
| validate_password.check_user_name    | ON     |
| validate_password.dictionary_file    |        |
| validate_password.length             | 8      |
| validate_password.mixed_case_count   | 1      |
| validate_password.number_count       | 1      |
| validate_password.policy             | MEDIUM |
| validate_password.special_char_count | 1      |
+--------------------------------------+--------+
```

- понижаем уровень проверки: `SET GLOBAL validate_password.length=7;`
- либо выполняем запрос в соответствии с требованиями

---

#### Ошибка: General error: 1419 You do not have the SUPER privilege and binary logging is enabled

1. Решение
- `set global log_bin_trust_function_creators=1;`

---

## Примеры

#### 1. Задача:

*Показать все значения из столбцов id, balance, в таблице users, где balance = 10*

Запрос:

`select id, balance from users where balance = 10`

Результат:
```
| id     | balance |
|--------|---------|
| 422    | 10.00   |
| 832    | 10.00   |
| 2966   | 10.00   |
| 4534   | 10.00   |
| 7391   | 10.00   |
| 10079  | 10.00   |
| 10535  | 10.00   |
| 11575  | 10.00   |
| 12077  | 10.00   |
| 12173  | 10.00   |
| 15459  | 10.00   |
| 15739  | 10.00   |
| 17237  | 10.00   |
| 157937 | 10.00   |
```

#### 2. Задача:

*Показать все значения из столбцов id, balance, в таблице users, где email содержит слово test и balance > 1000*

Запрос:

`select id, balance from users where email like '%test%' and balance > 1000`

Результат:
```
| id     | balance    |
|--------|------------|
| 1      | 9999669.00 |
| 20148  | 8377.00    |
| 157509 | 5580.00    |
| 157521 | 887676.00  |
| 157532 | 10970.00   |
| 157587 | 99709.00   |
| 157752 | 10013.00   |
| 157819 | 99200.00   |
| 157821 | 1022.00    |
| 157888 | 10000.00   |
| 157892 | 2137.00    |
| 157900 | 1710.00    |
| 157921 | 99803.00   |
```

#### 3. Задача:

*Показать значение столбца utm_source с группировкой по количеству*

Запрос:

`select utm_source, count(*) from users group by utm_source`

Результат:
```
| utm_source | count(*) |
|------------|----------|
| <null>     | 4934     |
| source77   | 1        |
| src2       | 1        |
| tg_office  | 1        |
| test       | 3        |
| 129        | 2        |
| R          | 4        |
| rsy_mb7    | 1        |
| rsy_mb5    | 1        |
| bhw        | 97       |
| affbank    | 56       |
| FBK        | 1        |
| cparip     | 10       |
```

#### 4. Задача:

*Сортировка результатов. По умолчанию сортирует по возрастанию. Для сортировки по убыванию необходимо добавить desc*

Запрос:

`select id, balance from users where balance > 100000 order by balance`

Результат:
```
| id     | balance       |
|--------|---------------|
| 3788   | 131100.00     |
| 4666   | 216400.00     |
| 3504   | 626450.00     |
| 157521 | 887676.00     |
| 1      | 9999669.00    |
| 15753  | 3243234234.00 |
```

#### 5. Задача:

*Получить сумму значений в столбце num, для записей у которых столбец date=2021-04-01*

Запрос:

`select sum(num) from stat_account where date='2021-04-01'`

Результат:
```
| sum(num) |
|----------|
| 1702     |
```

#### 6. Задача:

*Вывести дубликаты записей (одинаковую сумму баланса) с группировкой по сумме и количеством одинаковых дубликатов*

Запрос:

`select balance, count(*) as count from users group by balance having count(*) > 1 order by count`

Результат:
```
| balance       | count |
|---------------|-------|
| 1000.00000000 | 2     |
| 751.00000000  | 2     |
| 8.00000000    | 4     |
| 100.00000000  | 4     |
| 500.00000000  | 5     |
| 6.00000000    | 5     |
| 7.00000000    | 6     |
| 5.00000000    | 6     |
| 97.00000000   | 6     |
| 1.00000000    | 7     |
| 997.00000000  | 12    |
| 10.00000000   | 15    |
| 2.00000000    | 23    |
| 3.00000000    | 35    |
```

#### 7. Задача:

*Вывести размер баз данных*
  
Запрос:
  
```mysql
SELECT table_schema "DB Name", 
Round(Sum(data_length + index_length) / 1024 / 1024, 1) "DB Size in MB" 
FROM   information_schema.tables 
GROUP  BY table_schema; 
```

Результат:

```
| DB Name               | DB Size in MB |
| --------------------- | ------------- |
| mysql                 | 3.7           |
| information_schema    | 0.0           |
| db_name1              | 697.5         |
| db_name2              | 1.9           |
| db_name3              | 4971.5        |
| db_name4              | 2.1           |
| db_name5              | 4316.2        |
| db_name6              | 7702.3        |

```

#### 8. Задача:

*Вывести размер таблиц в конкретной базе данных*

Запрос:

```mysql
SELECT
table_name AS "Table",  
round(((data_length + index_length) / 1024 / 1024), 2) as size   
FROM information_schema.TABLES  
WHERE table_schema = "YOUR_DATABASE_NAME"  
ORDER BY size DESC; 
```

Результат:

```
| Table    | size    |
| -------- | ------- |
| tb_name1 | 2210.28 |
| tb_name2 | 2110.20 |
| tb_name3 | 323.98  |
| tb_name4 | 315.97  |
| tb_name5 | 4.33    |
| tb_name6 | 2.52    |
| tb_name7 | 1.59    |
```

---

#### 9. Задача:

*Вывести список кодировок таблиц для указанной базы*

Запрос:

```mysql
SELECT
    TABLE_NAME,
    TABLE_COLLATION,
    TABLE_SCHEMA
FROM information_schema.TABLES
WHERE TABLE_SCHEMA IN ( 'db_name')
```

#### 10. Задача:

*Посчитать количество записей и сгруппировать по дате (дата хранится в формате Unix)*

Запрос:

```mysql
SELECT DATE(FROM_UNIXTIME(created_at)) AS created_at,
       COUNT(*) AS NumRow
FROM   user
GROUP BY DATE(FROM_UNIXTIME(created_at))
ORDER BY created_at
```

#### 11. Задача:

*Вывести записи, которые были добавлены в определенную дата и добавлялись в течении последующей недели*

Запрос:

```mysql
select *
from orders
where tm_create between '2022-01-16 00:00:00' and '2022-01-16 23:59:59' + interval 1 week
```

#### 12. Задача

*Обновление колонки с двумя join*

```mysql
update card_auto_refills
    join cards on card_auto_refills.card_id = cards.id
    join users on cards.user_id = users.id
set card_auto_refills.active = 0
where users.id = 1
```

#### 13. Задача

*Сформировать ссылку на кабинет пользователя, посчитать кол-во его карт и дату последней транзакции*

```mysql
select concat('https://lk.site.com/user/', id, '/edit') as url,
       cards_count,
       (select processed_at from transactions where id = (
           select max(id) from transactions where user_account_id in(
               select id from user_accounts where user_id = t1.id
           )
       )) t_processed_at
from (
         select u.id,
                count(c.id) cards_count,
                sum(case when c.description is not null then 1 else 0 end) c_type
         from users u
                  join cards c on c.user_id = u.id
         where u.type = 0
         group by u.id
         having c_type > 10
         order by count(c.id) desc
     ) t1
```

#### 14. Задача

*Среднее количество дней действия игрового аккаунта с группировкой по его типу*

```mysql
select game_accounts.type, format(avg(datediff(game_accounts.deleted_at, game_accounts.created_at)), 0) as avg_days
from game_accounts
group by game_accounts.type
order by avg_days desc
```