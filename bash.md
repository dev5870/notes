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
#!/bin/bash
# левый верхний
gnome-terminal --geometry=57x26+0+0
# левый нижний
gnome-terminal --geometry=57x26+0-20
# правый верхний
gnome-terminal --geometry=101x26-2320+0
# правый нижний
gnome-terminal --geometry=101x26-2320-20
```

### 3. Очистка (рекурсивно) файлов по расширению

```bash
#!/bin/bash

# Путь к папке с файлами .log
logs_dir="/home/user/workspace/project/storage/logs"

# Поиск всех файлов .log в указанной папке
log_files=$(find "$logs_dir" -type f -name "*.log")

# Очистка каждого файла с помощью команды echo > file.log
for file in $log_files; do
  echo > "$file"
done
```
