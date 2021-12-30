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

---

#### Локальное тестирование Telegram бота с помощью ngrok

1. Запускаем локальный проект через ngrok: `ngrok http -host-header=rewrite site.com`
   - установка ngrok описана [здесь](https://github.com/kostyashelest/notes/blob/master/ubuntu.md#%D0%BB%D0%BE%D0%BA%D0%B0%D0%BB%D1%8C%D0%BD%D1%8B%D0%B9-%D1%81%D0%B5%D1%80%D0%B2%D0%B5%D1%80-%D0%B4%D0%BE%D1%81%D1%82%D1%83%D0%BF%D0%BD%D1%8B%D0%B9-%D0%B2-%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D0%BD%D0%B5%D1%82%D0%B5-ngrok)
2. Берем адрес ngrok и проставляем его в вубхук: `https://api.telegram.org/bot{your_token}/setWebhook?url=https://add.ngrok.io/api/tg-bot`
   - адрес ngrok указывать с https протоколом 
   - указывать точный путь к api
   - не будет работать с включенным vpn

---

#### Структура telegram данных для тестирования бота по api через postman

- без callback секции:

```json
{
  "update_id": 12345678,
  "message": {
    "message_id": 111,
    "from": {
      "id": 77777777,
      "is_bot": false,
      "first_name": "Test",
      "username": "David",
      "language_code": "ru"
    },
    "chat": {
      "id": 77777777,
      "first_name": "Test",
      "username": "David",
      "type": "private"
    },
    "date": 1640776799,
    "text": "/start",
    "entities": [
      {
        "offset": 0,
        "length": 6,
        "type": "bot_command"
      }
    ]
  }
}
```

- с callback секцией:

```json
{
  "update_id": 12345678,
  "callback_query": {
    "id": "11111111111111111111111",
    "from": {
      "id": 77777777,
      "is_bot": false,
      "first_name": "David",
      "username": "Test",
      "language_code": "ru"
    },
    "message": {
      "message_id": 111,
      "from": {
        "id": 22222222222,
        "is_bot": true,
        "first_name": "bot_name",
        "username": "NameBot"
      },
      "chat": {
        "id": 77777777,
        "first_name": "David",
        "username": "Test",
        "type": "private"
      },
      "date": 1640790944,
      "text": "Button name on telegram:",
      "reply_markup": {
        "inline_keyboard": [
          [
            {
              "text": "userName",
              "callback_data": "test_data"
            }
          ],
          [
            {
              "text": "userName2",
              "callback_data": "test_data2"
            }
          ]
        ]
      }
    },
    "chat_instance": "33333333333333333333333",
    "data": "test_data2"
  }
}
```