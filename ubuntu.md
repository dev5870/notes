
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

1. Редактирование процессов cron (текущего пользователя):

  `crontab -e`

  *Важно! Имеет значение из под какого пользователя выполняется запуск.*

2. Редактирование процессов cron (другого пользователя):

  `crontab -e -u www-data`

3. Просмотр запущенных процессов (текущего пользователя):

  `crontab -l`

4. Просмотр запущенных процессов (другого пользователя):

  `crontab -l -u www-data`

5. Просмотр логов:

  `grep CRON /var/log/syslog`

6. Вывод ошибок в файл:

  `* * * * * /home/user/bin start 2>>/home/user/workspace/er.log`

---

#### Создание файла произвольного размера

`fallocate -l 10M test.txt`

---

#### Добавление времени в терминал

![отображения времени в терминале](https://raw.githubusercontent.com/kostyashelest/notes/master/img/ubuntu_time_terminal.png)

- Вариант #1
  - В ~/.bashrc добавляем (отдельной строкой):

    `export PROMPT_COMMAND="echo -n \[\$(date +%H:%M:%S)\]\ "`

  - Делаем перезагрузку

    `source ~/.bashrc`

    *В некоторых случаях данный способ может ломаться*

- Вариант #2
  - В ~/.bashrc добавляем:

    `PS1='[$(date +%m/%d/%y)]` - выводит дату

    `PS1='[$(date +%H/%M/%S)]` - выводит время

    `PS1='\[\033[01;34m\][$(date +%H:%M)]` - выводит время синим цветом
    
  - Делаем перезагрузку

    `source ~/.bashrc`

---

#### Добавление ветки git в терминал

![отображения времени в терминале](https://raw.githubusercontent.com/kostyashelest/notes/master/img/ubuntu_github_flow_terminal.png)
- В ~/.bashrc добавляем:

  `PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\[\033[01;32m\]$(__git_ps1)\[\033[00m\]\$ '`

- Делаем перезагрузку

  `source ~/.bashrc`
