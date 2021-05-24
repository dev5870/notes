# BASH

---

### 1. Запуск bash скрипта с помощью команды:

В домашней директории создать папку:

`mkdir ~/bin`

Перенести скрипт в папку:

`cp fileName ~/bin/file`

*файл должен быть исполняемым (sudo chmod +x file)*

В оболочку (файл .bashrc) добавляем строку:

`export PATH=~/bin/file:$PATH`

Делаем перезагрузку

`source ~/.bashrc`

### 2. Запуск 4 окон терминала:

```
gnome-terminal --geometry=101x26-925+0
gnome-terminal --geometry=101x26+0-20
gnome-terminal --geometry=101x26-0-20
gnome-terminal --geometry=101x26-0-925
```
