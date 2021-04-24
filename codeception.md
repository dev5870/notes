## Codeception

---

### 1 Установка

- Стандартно, через composer:

  `composer require "codeception/codeception" --dev`

  Подробнее: https://codeception.com/quickstart

### 2 Основные команды

- 2.1 Генерация теста:

  `vendor/bin/codecept generate:test unit Example`

- 2.2 Запуск конкретного класса с тестами:

  `vendor/bin/codecept run unit ExampleTest`

- 2.3 Добавляем вывод шагов теста:

  `vendor/bin/codecept run unit ExampleTest --steps`

- 2.4 Запуск конкретного теста в классе:

  `vendor/bin/codecept run acceptance UserRegistrationCest:ensureThatSuccessfulRegistrationWorks`

- 2.5 Включаем дебагер:

  `vendor/bin/codecept run unit Test --steps --debug`

- 2.6 Выводим в консоль данные из кода (объект, массив и тд):

  `codecept_debug(User::findIdentity(100));`

- 2.7 Обновляем данные в БД:

  `$I->updateInDatabase('users', array('is_vip' => 0), array('email' => 'autotest+432418994@testacc.ru'));`

  *В первом массиве указываем `что меняем`, во втором `у кого меняем`*

- 2.8 Обход reCAPTCHA во время тестов:
> https://developers.google.com/recaptcha/docs/faq

### 3 Модули

#### 3.1 Модуль WebDriver

- 3.1.1 Для запуска приемочных тестов в браузере:

  Устанавливаем модуль webdriver через composer:

  `composer require --dev codeception/module-webdriver`

  Рабочий конфиг для suite (отступы имеют значение):
```
class_name: AcceptanceTester
modules:
    enabled:
        - WebDriver:
            url: http://your.domain/
            browser: firefox
            pageload_timeout: 20
            path: ''
            clear_cookies: true
            window_size: maximize
            capabilities:
             acceptInsecureCerts: true
```

- 3.1.2 Устанавливаем драйвер для браузера firefox:

  `sudo apt install firefox-geckodriver`

- 3.1.3 Запуск тестов:

  Запускаем драйвер браузера:

  `geckodriver`

  Profit: Запускаем тесты.

#### 3.2 Модуль PhpBrowser

- 3.2.1 Рабочий конфиг (отступы имеют значение):
```
class_name: AcceptanceTester
modules:
    enabled:
        - PhpBrowser:
            url: http://your.domain/
```

#### 3.3 Модуль Db

- 3.3.1 Рабочий конфиг (отступы имеют значение):
```
class_name: AcceptanceTester
modules:
    enabled:
        - Db:
            dsn: mysql:host=localhost;dbname=name
            user: user
            password: "12345"
```

#### 3.4 Модуль REST

- 3.4.1 Рабочий конфиг в связке с другими модулями:
```
class_name: ApiTester
modules:
   enabled:
       - REST:
           depends: PhpBrowser
           url: &url 'http://your.domain/' # you only need the &url anchor for further PhpBrowser configs
           shortDebugResponse: 300 # only the first 300 chars of the response
       - Db:
           dsn: mysql:host=localhost;dbname=name
           user: user
           password: "12345"
   config:
       PhpBrowser:
           url: *url # repeats the URL from the REST module; not needed if you don't have further settings like below
           headers:
               Content-Type: application/json
```

- 3.4.2 Примеры API тестов для разных методов:
```
<?php
use yii\helpers\Url as Url;
class ApiCest
{
    public function ShowsUsersProxyCest(ApiTester $I)
    {
      $I->wantTo('GET - ​/api​/v1​/proxies​/{id} - Shows users proxy');
      $I->amBearerAuthenticated(11);
      codecept_debug('получаем массив всех активных proxy (с трафиком)');
      codecept_debug($allProxy = $I->grabColumnFromDatabase('traffic', 'proxy_id', array('tm !=' => null)));
      codecept_debug($idProxy = end($allProxy));
      $I->sendGet('/proxies/'.$idProxy);
      $I->seeResponseCodeIs(\Codeception\Util\HttpCode::OK);
    }

    public function df(ApiTester $I)
    {
      $I->wantTo('POST - /api​/v1​/proxies - Add new user\'s proxy');
      $I->amBearerAuthenticated(11);
      $I->sendPost('/proxies', [
        'country_id' => 1149361,
        'type_id' => 'static_residential',
        'alldomains' => 1,
        'whitelist' => '127.0.0.1'
       ]);
      $I->seeResponseCodeIs(201);
    }

    public function MarkUserProxyAsDeletedCest(ApiTester $I)
    {
      $I->wantTo('DELETE - /api​/v1​/proxies - Mark user proxy deleted');
      $I->amBearerAuthenticated(11);
      codecept_debug('получаем массив всех активных proxy');
      codecept_debug($allProxy = $I->grabColumnFromDatabase('proxies', 'id', array('status' => 'active')));
      codecept_debug($idProxy = end($allProxy));
      $I->sendDelete('/proxies/'.$idProxy);
      $I->seeResponseCodeIs(204);
    }

    public function UpdateUserProxyCest(ApiTester $I)
    {
      $I->wantTo('PUT - /api​/v1​/proxies - Update user proxy');
      $I->amBearerAuthenticated(11);
      codecept_debug('получаем массив всех активных proxy');
      codecept_debug($allProxy = $I->grabColumnFromDatabase('proxies', 'id', array('status' => 'active', 'user_id' => 11)));
      codecept_debug($idProxy = end($allProxy));
      $I->sendPut('/proxies/'.$idProxy, [
        'alldomains' => 0,
        'domains' => 'vk.com',
        'auth_type' => 'whitelist',
        'whitelist' => '127.0.0.1'
       ]);
      $I->seeResponseCodeIs(\Codeception\Util\HttpCode::OK);
    }
}
```

#### 3.5 Модуль Cli

- 3.5.1 Рабочий конфиг в связке с другими модулями:
```
class_name: AcceptanceTester
modules:
    enabled:
        - Asserts:
        - Cli:
        - PhpBrowser:
            url: http://your.domain
        - Db:
            dsn: mysql:host=localhost;dbname=name
            user: name
            password: "12345"
```

#### 3.6 Модуль Asserts

- 3.6.1 Рабочий конфиг указан выше

### 4 Дополнения

#### 4.1 Allure Codeception

- **4.1.1 Установка**

  Выполняем команду:

  `sudo apt install allure`

  - *Отчеты генерируются в .xml формате (tests/_output/allure-results)*

  Для генерации и запуска красивых отчетов в браузере необходимо:

  - *Скачать и распаковать архив allure2 https://bintray.com/qameta/maven/allure2*

  В composer.json добавляем:
```
"require-dev": {
    "allure-framework/allure-codeception": ">=1.1.0"
},
```

  В codeception.yml добавляем:
```
extensions:
    enabled:
        - Yandex\Allure\Codeception\AllureCodeception
    config:
        Yandex\Allure\Adapter\AllureAdapter:
            deletePreviousResults: false
            outputDirectory: allure-results
```

  Выполняем:

  `composer update allure-framework`

- **4.1.2 Генерация и запуск Allure отчетов**

  Генерация отчета (без предварительного сохранения истории):

  `/home/user/workspace/allure/bin/allure serve /home/user/workspace/your.domain/tests/_output/allure-results/`

  Генерация отчета (с предварительным сохранением истории):

  Сперва генерируем отчет:

  `/home/user/workspace/allure/bin/allure generate /home/user/workspace/your.domain/tests/_output/allure-results/`

  Переносим сгенерированную историю в проект:

  `cp -r allure-report/history/ /home/user/workspace/your.domain/tests/_output/allure-results/history/`

  Открываем сгенерированный отчет:

  `/home/user/workspace/allure/bin/allure open allure-report/`

- **4.1.3 BASH скрипт для автоматизации генерации и запуска отчетов**

  *Скрипт для генерации, копирования истории и запуска отчета. Можно использовать для нескольких сайтов.*

  Скрипт в репозитории:

  https://github.com/kostyashelest/bash/blob/master/scripts/allure

### 5 HELPERS

- **5.1 Создание собственного Helper файла**

  Создаем helper:

  `vendor/bin/codecept generate:helper helper_name`

- **5.2 Конфиг suite файла**

  *В конфиг необходимо подключить созданный helper файл.*

      class_name: AcceptanceTester
      modules:
          enabled:
              - \Helper\helper_name

  Выполняем build:

  `vendor/bin/codecept build`

- **5.3 Используем базу данных в helper файле**

      <?php
      namespace Helper;
      class User extends \Codeception\Module
      {
        public function findAdminEmail($id)
        {
          $db = $this->getModule("Db");
          return $db->grabColumnFromDatabase('users', 'email', array('id' => $id));
        }
      }
