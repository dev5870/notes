# Git

---

1. PULL ветки master в локальную ветку master:  
    `git pull origin master`
   

2. PULL удаленной ветки в локальную ветку:  
    `git pull origin dfdev-1844`
   

3. Создание и переключение на новую ветку:  
    `git checkout -b dfdev-1844`
   
- *NOTE: Имеет значение с какой ветки создаем и переходим! Предварительно переходим в master*


4. PUSH локальной ветки в удаленный репозиторий:  
    `git push origin dfdev-codeception`


5. Удаление локальной ветки:  
    `git branch -d dfdev-seoOpitmize`

- *если есть неслитые изменения, то:*  
`git branch -D dfdev-seoOpitmize`

  
6. Спрятать изменения:  
- *Если файлы не добавлены в индекс:*  
    `git stash save -u`

- *Если файлы в индексе:*  
    `git stash save`

- *Вернуться к работе:*  
    `git stash pop`


7. Слияние веток:  
- *Переключаемся на ветку в которую сливаем:*  
`git checkout dfdev-codeception`

- *Сливаем в ветку dfdev-codeception ветку dfdev-1497:*  
`git merge dfdev-1497`
  

8. Отмена слияния веток:  
`git reflog`

- *Находите хэш коммита, к которому хотите вернуть изменения. Будет что-то вроде "8f05e00 HEAD@{4}: checkout: moving from
master to sphere" или "4c31200 HEAD@{10}: commit: Awesome feature implemented."*  
`git reset --hard [нужный хэш]`


9. FETCH  
`git fetch`

- *Как git pull, только без merge. Fetch подтягивает удаленные ветки, но не объединяет их с локальными.*


10. Изменить описание последнего коммита  
    `git commit --amend -m "New commit"`
