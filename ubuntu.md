
# Ubuntu

---

#### ОСНОВНОЕ

| Команда | Описание |
| ------------- | ------------- |
| `sudo cp /dev/null filename`  | Очистить файл через терминал  |
| `rm -rf dir_name/*` | Очистить директорию (без удаления директории)  |
| `tail -1 filename.txt` | Вывести последнюю одну строку файла |
| `scp -P4141 /Users/kosmos/u0364535_testlin.sql kosmos@194.58.103.125:/home/kosmos` | копирование файлов с пк на сервер |
| `cp /home/что_копируем/ /home/куда_копируем/` | копирование файлов на сервере |
| `mv /имя_папки_1/файл_1 /имя_папки_2/` | перемещение файлов внутри сервера |
| `mv /имя_папки_1/файл_1 /имя_папки_2/файл_2` | перемещение и переименовывание файла внутри сервера |
| `mv /имя_папки_1/файл_1 /имя_папки_1/файл_2` | просто переименовать файл |
| `iconv -f CP1251 -t UTF-8 1.txt > 2.txt` | смена кодировки файла |
| `sudo sysctl -w net.inet.ip.ttl=65` | для обхода блокировки на раздачу интернета с мобильного |
| `zip -r имя_архива архивируемая_папка` | создание архива |
| `du -sh *` | вывод списка папок и файлов с указанием их размера |
| `sed 's/ /%20/g' key.txt` | замена пробела на символы %20 для каждой строки (g) в конкретном файле |
| `awk '{print "text"$0}' key.txt` | добавление текста в начало каждой строки |
| `awk '{print $0"text"}' file.txt` | добавление текста в конец строки |
| `tr ' ' '\n' < FILEname` | меняем пробел на перенос строки |
| `chmod +x name.sh` | преобразовываем файл в исполняемый bash скрипт |
| `nohup ./name.sh &` | запуск bash скрипта в фоне |
| `history -cw` | очистить историю ssh |
| `pwd` | полный путь к текущей директории |
| `ssh -p 4110 userName@193.124.000.000` | Подключение к серверу по определенному порту |
| `sudo chown omlook:www-data -R site.ru/` | смена владельца |
| `cat file.txt \| wc -l` | подсчет количества строк в файле |
| `grep "a" file.txt \| wc -w` | подсчет количества вхождений в файле |
| `wget -r -k -l 7 -p -nc -erobots=off --user-agent="Mozilla/5.0 (Macintosh; Intel Mac OS X 10.8; rv:21.0) Gecko/20100101 Firefox/21.0" site.ru` | wget |
| `touch fileName.txt` | создание файла |
| `dig site.ru txt` | проверка записей txt домена |
| `dig site.ru mx` | проверка записей mx домена |
| `fallocate -l 10M test.txt` | Создание файла произвольного размера |

---

### FIND

| Команда | Описание |
| --- | --- |
| `find /var/www/ -type f -exec chmod 0644 {} \;` | замена прав на файлы |
| `find /var/www/ -type d -exec chmod 0755 {} \;` | замена прав на папки |
| `find . -name "*.html-r" -type f` | поиск рекурсивно по расширению файла и вывод найденных результатов |
| `find . -name "*.html-r" -type f -delete` | поиск и удаление рекурсивно по расширению файла |
| `find . -type f -name '*.php2' -exec sed -i -r 's/что_нужно_заменить/на_что_нужно_заменить/g' {} \;` | поиск и замена рекурсивно внутри файлов |
| `find ./ -type f -exec rename -v 's/html/php/' {} \;` | массовая рекурсивная замена расширения файла с html на php |

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

---

#### Изменение локального IP адреса (127.0.0.1)

- Выполняем `ifconfig`  
![Изменение локального IP адреса (127.0.0.1)](https://raw.githubusercontent.com/kostyashelest/notes/master/img/localip.png)  
- Далее: `sudo service network-manager stop`   
- Указываем новый IP: `sudo ifconfig lo 127.0.0.2`  
- Запускаем: `sudo service network-manager start`