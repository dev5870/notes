# PHPUnit

---

## 1 PHPUnit в Laravel

### 1.1 Основное

- конфиг файл в корне проекта - `phpunit.xml`
- запуск группы тестов (suite) - `vendor/bin/phpunit --filter 'tests\\Feature\\User'`
- запуск конкретного теста:
  - `vendor/bin/phpunit --filter 'tests\\Feature\\Admin\\ContentTest::test_create_content'`
  - `vendor/bin/phpunit --filter methodName path/to/file.php`
- использование транзакций (для отката БД к первоначальному состоянию) - `use DatabaseTransactions;`
- использование фейкеров - `use WithFaker;`, далее обращаемся к фейкеру: `$this->faker->email;`
- запуск всех тестов:
  - `vendor/bin/phpunit`
  - `php artisan test`

### 1.2 Настройка БД

- Изначально настройки для БД берутся из phpunit.xml:

```
         <server name="DB_CONNECTION" value="sqlite"/>
         <server name="DB_DATABASE" value=":memory:"/>
```

- Если строки закомментированы, берутся настройки из конфига указанного в phpunit.xml:

```
        <server name="APP_ENV" value="testing"/>
```

- То есть, из файла `.env.testing`, если такой файл отсутствует берётся информация из `.env`
