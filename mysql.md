# MySQL

---

#### Основные команды

| Команда | Описание |
| ------------- | ------------- |
| `mysql -u root -p`  | Авторизация под пользователем root  |
| `mysql.server start` | Start mysql на macos  |
| `sudo service mysql start/restart/stop` | Старт, рестарт, стоп mysql в Ubuntu |
| `mysqldump -uroot -p db_name > file_name.sql` | Бэкап базы данных |
| `mysql db_name -u user_name -p < dump.sql` | Залить базу на сервер mysql |
| `show databases` | Показать список всех баз данных |
| `use db_name` | Переход в определенную базу данных |
| `show tables` | Показать все таблицы в базе данных |
| `show columns from table_name` | Показать все столбцы в таблице |
| `select count(*) from table_name` | Считаем количество записей в таблице |
| `truncate table tb_name` | Очистить таблицу |

#### CREATE

| Команда | Описание |
| ------------- | ------------- |
| `create database db_name` | Создание базы данных |
| `create user 'userName'@'localhost' identified by 'password'` | Создание пользователя БД |

#### UPDATE

| Команда | Описание |
| ------------- | ------------- |
| `update ips set tm_last_seen='2022-05-23 18:08:58'` | Обновить таблицу ips, установить всем значениям в столбце `tm_last_seen` = дате |
| `update users set users.email = users.id` | Присвоить значение столбца `id` столбцу `email` в таблице `users` |

#### DROP

| Команда | Описание |
| ------------- | ------------- |
| `drop user 'userName'@'localhost'` | Удаление пользователя БД |

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
  
```
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

```
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