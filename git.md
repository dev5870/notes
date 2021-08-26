# Git

---

#### Основное

| Команда | Описание |
| ------- | -------- |
| `git pull origin master` | PULL ветки master в локальную ветку master |
| `git pull origin dfdev-1844` | PULL удаленной ветки в локальную ветку |
| `git checkout -b dfdev-1844` | Создание и переключение на новую ветку. *NOTE: Имеет значение с какой ветки создаем и переходим! Предварительно переходим в master* |
| `git push origin dfdev-codeception` | PUSH локальной ветки в удаленный репозиторий |
| `git branch -d dfdev-seoOpitmize` | Удаление локальной ветки |
| `git push origin :old_branch ` | Удаление Remote ветки |
| `git stash save -u` | Спрятать изменения, если файлы не в индексе |
| `git stash save` | Спрятать изменения, если файлы в индексе |
| `git stash pop` | Вернуть изменения к работе |
| `git branch --merged master -a` | Отобразить список слитых в мастер веток (локальные и удаленные) |
| `git fetch` | Как git pull, только без merge. Fetch подтягивает удаленные ветки, но не объединяет их с локальными. |
| `git commit --amend -m "New commit"` | Изменить описание последнего коммита |
| gitignore через exclude | В файле `.git/info/exclude` можно добавлять правила |
| `git remote show origin` | Показать remote url |
| `git remote set-url origin new.git.url/here` | Установить новый remote origin url |
| `git log origin/branch-name..HEAD` | Просмотр незапушенных комитов |
| `git branch -m old_branch_name new_branch_name` | Переименовать ветку |

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