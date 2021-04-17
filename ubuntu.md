
### Ubuntu

---

#### Основное

1. Очистить файл через терминал:

`sudo cp /dev/null filename`

2. Очистить директорию (без удаления директории):

`rm -rf dir_name/*`

---

#### CURL

1. Тестирование проксей (без авторизации) с помощью curl:

`curl -x "socks5h://server-name:port" 2ip.ru`

2. Тестирование проксей (с авторизацией) с помощью curl:

*формат 1:* `curl -x "socks5h://user-login:password@server-name:port" 2ip.ru`

*формат 2:* `curl -x "socks5h://server-name:port" -u auser-login:password 2ip.ru`

*формат 3:* `curl -x "http://user-login:password@server-name:port" 2ip.ru`

---

#### CRON

1. Редактирование процессов в cron:

`crontab -e`

*Важно! Имеет значение из под какого пользователя выполняется запуск.*

2. Просмотр запущенных процессов:

`crontab -l`

3. Просмотр логов:

`grep CRON /var/log/syslog`

4. Вывод ошибок в файл:

`* * * * * /home/user/bin start 2>>/home/user/workspace/er.log`

---
