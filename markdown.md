# Markdown

---

#### 1  Изображения
  -  1.1 Вставка изображения в репозиторий GitHub
```
![Иллюстрация к проекту](https://github.com/jon/coolproject/raw/master/image/image.png)
![Image alt](https://github.com/{username}/{repository}/raw/{branch}/{path}/image.png)
{username} — ваш ник на ГитХабе;
{repository} — репозиторий где хранятся картинки;
{branch} — ветка репозитория;
{path} — путь к месту нахождения картинки.
```

#### 2 Диаграммы

 ```ditaa {cmd=true args=["-E"]}
  +----------------+   +----------------+    +----------------+
  | block_schema_1 |   | block_schema_2 |    | block_schema_3 |
  +-------+--------+   +-------+--------+    +-------+--------+
          |                    |                     |
          ˅                    ˅                     ˅
          +--------------------+---------------------+
                               |
                               ˅      
                       +-------+--------+
                       | block_schema_4 |
                       +----------------+
  ```
