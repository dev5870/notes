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
