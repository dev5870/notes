# Telegram

---

#### Создание бота

1. В поиске наберите **@botfather**, откройте родительского бота и нажмите "Start":

![telegram](https://raw.githubusercontent.com/kostyashelest/notes/master/img/tg_1.png)

2. Далее:
- Пишем команду /newbot, для создания нового бота.
- Придумываем имя бота.
- Придумываем ник бота.

![telegram](https://raw.githubusercontent.com/kostyashelest/notes/master/img/tg_2.png)

3. Если все прошло успешно, то увидите поздравления и токен вашего бота, в моем случае это:
- 341996777:AAHbnuvQib-vHU47i-6hbUrCU9D-qHYekxc
- Теперь нужно найти своего бота в поиске, указав его ник и нажать "Start", чтобы активировать его. В моем случае ник @DWS_MESSAGE_bot.

![telegram](https://raw.githubusercontent.com/kostyashelest/notes/master/img/tg_3.png)

4. После этого, нужно создать групповой чат, в который будут приходить заявки и пригласить туда нашего бота. Давайте займемся этим.
Зайдите в меню, нажмите "New Group" и задайте имя вашему чату.

![telegram](https://raw.githubusercontent.com/kostyashelest/notes/master/img/tg_4.png)

5. Не забываем пригласить своего бота в чат.

![telegram](https://raw.githubusercontent.com/kostyashelest/notes/master/img/tg_5.png)

6. На данный момент у нас есть бот, мы знаем его токен, есть чат, в который будут приходить заявки, и нам осталось узнать только id чата. Для этого, напишем в чате:
- /join @ник_бота

7. А затем, в браузере введем:
`https://api.telegram.org/botXXXXXXXXXXXXXXXXXXXXXXX/getUpdates`,  
где, `XXXXXXXXXXXXXXXXXXXXXXX` - токен вашего бота, полученный ранее.

Если все сделали правильно, то перед вами откроется подобная страница:

![telegram](https://raw.githubusercontent.com/kostyashelest/notes/master/img/tg_6.png)

8. Нас интересует объект `"chat":{"id":-209253141` - Это id моего тестового чата. На данном этапе у нас есть все, чтобы отправлять текстовые сообщение из контактной формы на сайте в Telegram.


9. ВНИМАНИЕ!
- В редких случаях, id чата может отображаться не сразу. Вместо этого, вы будете видеть: `{"ok":true,"result":[]}` Все нормально, не переживайте! Вы все сделали правильно. Просто подождите 10-15 минут и снова обновите страницу.
- Если по истечению 10-15 минут id чата не отображается, то попробуйте еще раз выполнить: найти своего бота в поиске, указав его ник и нажать "Start", чтобы активировать его.

---

#### Как узнать id чата или группы

1. Нужно добавить бота в чат/группу (для которой необходимо узнать id).
2. Написать в добавленный чат (писать через `/`, например: `/test`).
3. Перейти по ссылке: 
`https://api.telegram.org/botXXXXXXXXXXXXXXXXXXXXXXX/getUpdates`,  
где, `XXXXXXXXXXXXXXXXXXXXXXX` - токен вашего бота, полученный ранее.