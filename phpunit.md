# PHPUnit (Laravel)

---

## 1. Основное

### 1.1 Запуск тестов

- запуск группы тестов (suite) - `vendor/bin/phpunit --filter 'tests\\Feature\\User'`
- запуск конкретного теста:
  - `vendor/bin/phpunit --filter 'tests\\Feature\\Admin\\ContentTest::test_create_content'`
  - `vendor/bin/phpunit --filter methodName path/to/file.php`
- использование транзакций (для отката БД к первоначальному состоянию) - `use DatabaseTransactions;`
- использование фейкеров - `use WithFaker;`, далее обращаемся к фейкеру: `$this->faker->email;`
- запуск всех тестов:
  - `vendor/bin/phpunit`
  - `php artisan test`
- параллельный запуск тестов:
  - `./vendor/bin/paratest --runner WrapperRunner -p 16`
- анализ покрытия тестами (с формированием отчета):
  - `XDEBUG_MODE=coverage vendor/bin/phpunit --coverage-html /home/pc/workspace/www/site/report/`

### 1.2 Настройка БД

- конфиг файл в корне проекта - `phpunit.xml`
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

---

## 2. Готовые решения для тестов

### 2.1 Тест на загрузку файла в Laravel с PHPUnit

```php
/* @var User $user */
$user = User::factory()->create();
$user->refresh();
$this->actingAs($user);

Storage::fake('local');
$file = UploadedFile::fake()->create('image.jpg');

$response = $this->post(route($this->endpoint), [
    'file' => $file
]);

$response->assertCreated();
$response->assertJsonStructure([
    'data' => [
        'id',
        'user_id',
        'fileable_id',
        'fileable_type',
        'type',
        'title',
        'url',
    ]
]);
```