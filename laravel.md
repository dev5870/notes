# Laravel

---

### 1. Автоматическая очистка Laravel логов с помощью cron (Ubuntu):

Создаем bash скрипт `clear_logs.sh`:

```php
#!/bin/bash

log_dir="/home/user/workspace/api/storage/logs"

# Проверка существования директории логов
if [ -d "$log_dir" ]; then
  # Удаление файлов в директории логов
  find "$log_dir" -type f -delete
  echo "Логи в $log_dir очищены."
else
  echo "Директория $log_dir не существует."
fi
```

Сохраняем файл и делаем его исполняемым:

`chmod +x clear_logs.sh`

Открываем cron:

`crontab -e`

Добавляем строку:

`0 0 * * * /home/user/clear_logs.sh`

#### Не забываем везде указывать свои пути!