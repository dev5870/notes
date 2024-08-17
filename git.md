# Git

---

#### Основное

| Команда                                       | Описание                                                                                                                            |
|-----------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| `git pull origin master`                      | PULL ветки master в локальную ветку master                                                                                          |
| `git pull origin dfdev-1844`                  | PULL удаленной ветки в локальную ветку                                                                                              |
| `git checkout -b dfdev-1844`                  | Создание и переключение на новую ветку. *NOTE: Имеет значение с какой ветки создаем и переходим! Предварительно переходим в master* |
| `git push origin dfdev-codeception`           | PUSH локальной ветки в удаленный репозиторий                                                                                        |
| `git branch -d dfdev-seoOpitmize`             | Удаление локальной ветки                                                                                                            |
| `git push origin :old_branch `                | Удаление Remote ветки                                                                                                               |
| `git stash save -u`                           | Спрятать изменения, если файлы не в индексе                                                                                         |
| `git stash save`                              | Спрятать изменения, если файлы в индексе                                                                                            |
| `git stash pop`                               | Вернуть изменения к работе                                                                                                          |
| `git stash clear`                              | Очистить все спрятанные изменения                                                                                                   |
| `git branch --merged master -a`               | Отобразить список слитых в мастер веток (локальные и удаленные)                                                                     |
| `git fetch`                                   | Как git pull, только без merge. Fetch подтягивает удаленные ветки, но не объединяет их с локальными.                                |
| `git commit --amend -m "New commit"`          | Изменить описание последнего коммита                                                                                                |
| gitignore через exclude                       | В файле `.git/info/exclude` можно добавлять правила                                                                                 |
| `git remote show origin`                      | Показать remote url                                                                                                                 |
| `git remote set-url origin new.git.url/here`  | Установить новый remote origin url                                                                                                  |
| `git log origin/branch-name..HEAD`            | Просмотр незапушенных комитов                                                                                                       |
| `git branch -m old_branch_name new_branch_name` | Переименовать ветку                                                                                                                 |
| `git diff ветка1 ветка2`                      | Сравнение изменений между двумя ветками                                                                                             |
| `git diff --name-only ветка1 ветка2`          | Список измененных файлов                                                                                                            |
| `git diff --name-status ветка1 ветка2`        | Список измененных файлов со статусами (удален/изменен/добавлен)                                                                     |

---

#### Слияние веток:
- *Переключаемся на ветку в которую сливаем:*  
  `git checkout dfdev-codeception`

- *Сливаем в ветку dfdev-codeception ветку dfdev-1497:*  
  `git merge dfdev-1497`

---

#### Отмена слияния веток:

- Выводим лог:  
  `git reflog`

- *Находите хэш коммита, к которому хотите вернуть изменения. Будет что-то вроде "8f05e00 HEAD@{4}: checkout: moving from
  master to sphere" или "4c31200 HEAD@{10}: commit: Awesome feature implemented."*  
  `git reset --hard [нужный хэш]`
  
---

#### Отката последнего commit

- Откатываемся к предыдущему изменению: `git reset --hard 743acea`
- Делаем push: `git push origin branch_name --force`

---

#### Изменение файлов после коммита

*Если забыли добавить один из файлов в коммит.*

```
# Правим first.php и second.php
git add first.php
git commit 
# Вспоминаем что забыли добавить в коммит second.php
git add second.php
git commit --amend --no-edit
```

---

#### Git large files

Install

`sudo apt-get install git-lfs`

Init lfs

`git lfs install`

Track large file

`git lfs track large.json`

Then: `git add, commit, push`

Check large files

`git lfs ls-files`
