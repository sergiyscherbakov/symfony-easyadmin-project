# Symfony EasyAdmin Project

![PHP](https://img.shields.io/badge/PHP-8.1-777BB4?style=for-the-badge&logo=php&logoColor=white) ![Symfony](https://img.shields.io/badge/Symfony-6-000000?style=for-the-badge&logo=symfony&logoColor=white) ![MySQL](https://img.shields.io/badge/MySQL-8.0-4479A1?style=for-the-badge&logo=mysql&logoColor=white) ![EasyAdmin](https://img.shields.io/badge/EasyAdmin-4-FF6600?style=for-the-badge&logo=symfony&logoColor=white) ![Doctrine](https://img.shields.io/badge/Doctrine-3-FC6A31?style=for-the-badge&logo=doctrine&logoColor=white) ![Twig](https://img.shields.io/badge/Twig-3-339933?style=for-the-badge&logo=twig&logoColor=white) ![Composer](https://img.shields.io/badge/Composer-2.0-885630?style=for-the-badge&logo=composer&logoColor=white)

## Автор

**Розробник:** Сергій Щербаков
**Email:** sergiyscherbakov@ukr.net
**Telegram:** @s_help_2010

### 💰 Підтримати розробку
Задонатити на каву USDT (BINANCE SMART CHAIN):
**`0xDFD0A23d2FEd7c1ab8A0F9A4a1F8386832B6f95A`**

---

Проєкт для демонстрації роботи з Symfony Framework та EasyAdmin Bundle для створення адміністративної панелі з управлінням користувачами.

## Зміст

- [Встановлення необхідного програмного забезпечення](#встановлення-необхідного-програмного-забезпечення)
- [Створення проєкта](#створення-проєкта)
- [Структура проєкта](#структура-проєкта)
- [Налаштування бази даних](#налаштування-бази-даних)
- [Робота з проєктом](#робота-з-проєктом)
- [Тестування функціоналу](#тестування-функціоналу)

---

## Встановлення необхідного програмного забезпечення

### 1. Встановлення PHP

**Windows:**
1. Завантажте PHP з офіційного сайту: https://windows.php.net/download/
2. Рекомендована версія: PHP 8.1 або вище
3. Розпакуйте архів у папку `C:\php`
4. Додайте `C:\php` до змінної середовища PATH
5. Перевірка встановлення:
```bash
php -v
```

**Повинно вивести:**
```
PHP 8.1.x (cli) (built: ...)
```

### 2. Встановлення Composer

**Що таке Composer:**
Composer - це менеджер залежностей для PHP, який дозволяє управляти бібліотеками та пакетами у вашому проєкті.

**Встановлення на Windows:**
1. Завантажте Composer-Setup.exe з https://getcomposer.org/download/
2. Запустіть інсталятор
3. Виберіть шлях до php.exe (наприклад, `C:\php\php.exe`)
4. Завершіть встановлення
5. Перевірка встановлення:
```bash
composer -V
```

**Повинно вивести:**
```
Composer version 2.x.x
```

**Основні команди Composer:**
```bash
composer install       # Встановлює всі залежності з composer.lock
composer update        # Оновлює залежності до останніх версій
composer require       # Додає нову залежність до проєкту
composer dump-autoload # Оновлює автозавантажувач класів
```

### 3. Встановлення Symfony CLI (опціонально, але рекомендовано)

```bash
# Windows (через Scoop)
scoop install symfony-cli

# Або завантажте з https://symfony.com/download
```

Перевірка:
```bash
symfony -V
```

### 4. Встановлення MariaDB/MySQL

**MariaDB (рекомендовано):**
1. Завантажте з https://mariadb.org/download/
2. Встановіть MariaDB Server
3. Під час встановлення встановіть пароль для root (наприклад, `1234`)
4. Запам'ятайте порт (за замовчуванням: 3306)

**Перевірка встановлення:**
```bash
mysql --version
```

---

## Створення проєкта

### Крок 1: Створення нового Symfony проєкта

**Використовуючи Composer:**
```bash
# Створення повного веб-проєкту з усіма компонентами
composer create-project symfony/website-skeleton my_project

# Альтернативно: мінімальний проєкт
composer create-project symfony/skeleton my_project
```

**Використовуючи Symfony CLI:**
```bash
# Повний веб-проєкт
symfony new my_project --full

# Мінімальний проєкт
symfony new my_project
```

### Крок 2: Встановлення необхідних пакетів

```bash
cd my_project

# Встановлення EasyAdmin Bundle
composer require easycorp/easyadmin-bundle

# Встановлення Doctrine ORM (для роботи з базою даних)
composer require symfony/orm-pack

# Встановлення Doctrine Migrations (для міграцій БД)
composer require symfony/maker-bundle --dev
composer require doctrine/doctrine-migrations-bundle

# Встановлення Security Bundle (для автентифікації)
composer require symfony/security-bundle

# Встановлення Fixtures (для тестових даних)
composer require --dev doctrine/doctrine-fixtures-bundle
```

### Крок 3: Налаштування .env файлу

Відкрийте файл `.env` у кореневій папці проєкта:

```env
# .env
APP_ENV=dev
APP_SECRET=ce13cbebdf2d2a0fc5c8f2f616d09c95

# Налаштування бази даних
DATABASE_URL="mysql://root:1234@127.0.0.1:3306/symfony_admin_lab?serverVersion=mariadb-12.0.2&charset=utf8mb4"
```

**Пояснення параметрів DATABASE_URL:**
- `mysql://` - тип бази даних (MySQL/MariaDB)
- `root` - ім'я користувача БД
- `1234` - пароль користувача
- `127.0.0.1` - хост (localhost)
- `3306` - порт
- `symfony_admin_lab` - назва бази даних
- `serverVersion=mariadb-12.0.2` - версія сервера (замініть на свою)

---

## Структура проєкта

### Основні директорії та файли

```
my_project/
├── bin/                          # Виконувані скрипти
│   ├── console                   # Консольний інтерфейс Symfony
│   └── phpunit                   # Скрипт для запуску тестів
│
├── config/                       # Конфігураційні файли
│   ├── packages/                 # Конфігурація пакетів
│   │   ├── doctrine.yaml        # Налаштування Doctrine ORM
│   │   ├── framework.yaml       # Основні налаштування Symfony
│   │   ├── routing.yaml         # Налаштування маршрутизації
│   │   ├── security.yaml        # Налаштування безпеки та автентифікації
│   │   └── twig.yaml            # Налаштування шаблонізатора Twig
│   ├── routes/                   # Файли маршрутів
│   │   └── easyadmin.yaml       # Маршрути для EasyAdmin
│   ├── bundles.php               # Реєстрація встановлених бандлів
│   └── services.yaml             # Налаштування сервісів та DI
│
├── migrations/                   # Міграції бази даних
│   ├── Version20250919173155.php # Створення таблиці user
│   └── Version20250919174330.php # Додаткові зміни у БД
│
├── public/                       # Публічна директорія (доступна через веб)
│   ├── index.php                 # Точка входу додатка
│   └── bundles/                  # Статичні файли (CSS, JS, зображення)
│
├── src/                          # Вихідний код додатка
│   ├── Controller/               # Контролери
│   │   ├── Admin/
│   │   │   └── UserCrudController.php  # CRUD операції для User
│   │   ├── AdminController.php         # Головний контролер адмін-панелі
│   │   └── SecurityController.php      # Контролер автентифікації
│   │
│   ├── Entity/                   # Сутності (моделі даних)
│   │   └── User.php              # Сутність користувача
│   │
│   ├── Repository/               # Репозиторії (запити до БД)
│   │   └── UserRepository.php    # Репозиторій для User
│   │
│   ├── DataFixtures/             # Фікстури (тестові дані)
│   │   ├── AppFixtures.php       # Базовий клас фікстур
│   │   └── UserFixtures.php      # Фікстури користувачів
│   │
│   └── Kernel.php                # Ядро додатка
│
├── templates/                    # Шаблони Twig
│   ├── admin/                    # Шаблони адмін-панелі
│   │   ├── dashboard.html.twig   # Дашборд
│   │   └── index.html.twig       # Головна сторінка
│   ├── security/
│   │   └── login.html.twig       # Форма входу
│   └── base.html.twig            # Базовий шаблон
│
├── tests/                        # Тести
│   └── bootstrap.php             # Ініціалізація тестів
│
├── translations/                 # Переклади
│
├── var/                          # Тимчасові файли
│   ├── cache/                    # Кеш
│   └── log/                      # Логи
│
├── vendor/                       # Залежності Composer
│
├── .env                          # Змінні середовища (БД, секрети)
├── .env.test                     # Змінні для тестового середовища
├── .gitignore                    # Файли, що ігноруються Git
├── composer.json                 # Залежності проєкта
├── composer.lock                 # Заблоковані версії залежностей
└── symfony.lock                  # Symfony Flex lock файл
```

### Детальний опис ключових файлів

#### 1. `src/Entity/User.php`
**Призначення:** Сутність (модель) користувача для бази даних.

**Що містить:**
- Поля: `id`, `email`, `roles`, `password`
- Методи для роботи з автентифікацією
- Doctrine ORM атрибути для маппінгу з БД

**Основні методи:**
- `getId()` - отримання ID
- `getEmail()` / `setEmail()` - робота з email
- `getRoles()` / `setRoles()` - управління ролями
- `getPassword()` / `setPassword()` - робота з паролем
- `getUserIdentifier()` - ідентифікатор користувача для Symfony Security

#### 2. `src/Controller/AdminController.php`
**Призначення:** Головний контролер адміністративної панелі EasyAdmin.

**Що містить:**
- Маршрут `/admin` - точка входу в адмін-панель
- `configureDashboard()` - налаштування заголовка та вигляду дашборду
- `configureMenuItems()` - налаштування меню адмін-панелі

#### 3. `src/Controller/Admin/UserCrudController.php`
**Призначення:** Контролер для CRUD операцій з користувачами.

**Що містить:**
- Налаштування полів для створення/редагування користувачів
- Налаштування відображення списку користувачів
- Обробка форм

#### 4. `src/DataFixtures/UserFixtures.php`
**Призначення:** Завантаження тестових даних користувачів у БД.

**Що містить:**
- Метод `load()` для створення користувачів
- Хешування паролів
- Встановлення ролей (ROLE_ADMIN, ROLE_USER)

#### 5. `config/packages/doctrine.yaml`
**Призначення:** Налаштування Doctrine ORM.

**Що містить:**
- Підключення до бази даних
- Налаштування автоматичного маппінгу
- Режим розробки/продакшн

#### 6. `config/packages/security.yaml`
**Призначення:** Налаштування безпеки та автентифікації.

**Що містить:**
- Провайдери користувачів
- Файрволи (публічні/приватні зони)
- Налаштування входу/виходу
- Контроль доступу (access_control)

---

## Налаштування бази даних

### Крок 1: Створення бази даних

**Через команду Symfony:**
```bash
cd my_project
php bin/console doctrine:database:create
```

**Вручну через MySQL/MariaDB клієнт:**
```bash
mysql -u root -p
```

Введіть пароль (наприклад, `1234`), потім:
```sql
CREATE DATABASE symfony_admin_lab CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
SHOW DATABASES;
EXIT;
```

### Крок 2: Створення сутності User

```bash
php bin/console make:user User
```

**Відповіді на запитання:**
- Storing user data in a database? `yes`
- Email as unique identifier? `email`
- Will this app need to hash/check user passwords? `yes`

### Крок 3: Створення та виконання міграцій

**Створення міграції:**
```bash
php bin/console make:migration
```

**Виконання міграції:**
```bash
php bin/console doctrine:migrations:migrate
```

Підтвердіть виконання, натиснувши `yes`.

**Перевірка таблиць у БД вручну:**
```bash
mysql -u root -p symfony_admin_lab
```

```sql
SHOW TABLES;
-- Повинно показати: user, doctrine_migration_versions

DESCRIBE user;
-- Повинно показати поля: id, email, roles, password

SELECT * FROM user;
-- Покаже всіх користувачів (спочатку порожньо)

EXIT;
```

### Крок 4: Завантаження тестових даних (Fixtures)

**Створення fixtures:**
```bash
php bin/console make:fixtures UserFixtures
```

Відредагуйте файл `src/DataFixtures/UserFixtures.php`:

```php
<?php

namespace App\DataFixtures;

use App\Entity\User;
use Doctrine\Bundle\FixturesBundle\Fixture;
use Doctrine\Persistence\ObjectManager;
use Symfony\Component\PasswordHasher\Hasher\UserPasswordHasherInterface;

class UserFixtures extends Fixture
{
    private UserPasswordHasherInterface $passwordHasher;

    public function __construct(UserPasswordHasherInterface $passwordHasher)
    {
        $this->passwordHasher = $passwordHasher;
    }

    public function load(ObjectManager $manager): void
    {
        // Створення адміністратора
        $admin = new User();
        $admin->setEmail('admin@example.com');
        $admin->setRoles(['ROLE_ADMIN']);
        $admin->setPassword(
            $this->passwordHasher->hashPassword($admin, 'admin123')
        );
        $manager->persist($admin);

        // Створення звичайного користувача
        $user = new User();
        $user->setEmail('user@example.com');
        $user->setRoles(['ROLE_USER']);
        $user->setPassword(
            $this->passwordHasher->hashPassword($user, 'user123')
        );
        $manager->persist($user);

        $manager->flush();
    }
}
```

**Завантаження fixtures у БД:**
```bash
php bin/console doctrine:fixtures:load
```

Підтвердіть, натиснувши `yes`.

**Перевірка даних вручну:**
```bash
mysql -u root -p symfony_admin_lab
```

```sql
SELECT id, email, roles FROM user;
-- Повинно показати:
-- +----+-------------------+------------------+
-- | id | email             | roles            |
-- +----+-------------------+------------------+
-- |  1 | admin@example.com | ["ROLE_ADMIN"]   |
-- |  2 | user@example.com  | ["ROLE_USER"]    |
-- +----+-------------------+------------------+

EXIT;
```

---

## Робота з проєктом

### Запуск локального сервера

**Варіант 1: Використовуючи Symfony CLI (рекомендовано):**
```bash
cd my_project
symfony server:start
```

Сервер запуститься на `https://127.0.0.1:8000`

**Варіант 2: Використовуючи вбудований PHP сервер:**
```bash
cd my_project
php -S localhost:8000 -t public/
```

Сервер запуститься на `http://localhost:8000`

**Зупинка сервера:**
- Натисніть `Ctrl+C` у терміналі

### Створення контролерів

**Створення звичайного контролера:**
```bash
php bin/console make:controller HomeController
```

**Створення EasyAdmin CRUD контролера:**
```bash
php bin/console make:admin:crud
```

Виберіть сутність (наприклад, `User`).

### Робота з маршрутами

**Перегляд всіх маршрутів:**
```bash
php bin/console debug:router
```

**Перегляд інформації про конкретний маршрут:**
```bash
php bin/console debug:router admin
```

### Очищення кешу

```bash
# Очистити кеш
php bin/console cache:clear

# Очистити кеш в production
php bin/console cache:clear --env=prod
```

---

## Тестування функціоналу

### 1. Перевірка головної сторінки

**Тест:** Відкрийте у браузері `http://localhost:8000`

**Очікуваний результат:**
- Повинна відобразитися стартова сторінка Symfony
- Або сторінка 404 (якщо не створено головний маршрут)

### 2. Перевірка адміністративної панелі

**Тест:** Відкрийте у браузері `http://localhost:8000/admin`

**Очікуваний результат:**
- Повинна відкритися панель адміністратора EasyAdmin
- Відобразиться дашборд з заголовком "Admin Panel"
- У лівому меню будуть пункти:
  - Dashboard (з іконкою будинку)
  - Users (з іконкою користувачів)

**Що тестувати:**
1. **Перегляд списку користувачів:**
   - Клацніть "Users" у меню
   - Повинен з'явитися список користувачів
   - Кожен користувач показує: ID, Email, Roles

2. **Створення нового користувача:**
   - Клацніть кнопку "Create User"
   - Заповніть форму:
     - Email: `test@example.com`
     - Password: `test123`
     - Roles: Виберіть або введіть `["ROLE_USER"]`
   - Натисніть "Save"
   - Користувач з'явиться у списку

3. **Редагування користувача:**
   - У списку користувачів клацніть на іконку редагування (олівець)
   - Змініть email або ролі
   - Натисніть "Save"
   - Перевірте, що зміни збережені

4. **Видалення користувача:**
   - У списку користувачів клацніть на іконку видалення (кошик)
   - Підтвердіть видалення
   - Користувач зникне зі списку

**Перевірка через базу даних:**
```bash
mysql -u root -p symfony_admin_lab
```

```sql
-- Перегляд всіх користувачів
SELECT id, email, roles FROM user;

-- Перевірка конкретного користувача
SELECT * FROM user WHERE email = 'test@example.com';

-- Перевірка кількості користувачів
SELECT COUNT(*) FROM user;

EXIT;
```

### 3. Тестування автентифікації (якщо налаштована)

Якщо ви налаштували security для входу:

**Крок 1: Створення форми входу**
```bash
php bin/console make:auth
```

Виберіть:
- Authentication type: `1` (Login form authenticator)
- Controller class name: `SecurityController`
- Generate logout URL: `yes`

**Крок 2: Налаштування security.yaml**
Переконайтеся, що файл `config/packages/security.yaml` містить:

```yaml
security:
    password_hashers:
        App\Entity\User:
            algorithm: auto

    providers:
        app_user_provider:
            entity:
                class: App\Entity\User
                property: email

    firewalls:
        dev:
            pattern: ^/(_(profiler|wdt)|css|images|js)/
            security: false

        main:
            lazy: true
            provider: app_user_provider
            form_login:
                login_path: app_login
                check_path: app_login
                default_target_path: admin
            logout:
                path: app_logout
                target: app_login

    access_control:
        - { path: ^/admin, roles: ROLE_ADMIN }
        - { path: ^/login, roles: PUBLIC_ACCESS }
```

**Тест входу:**
1. Відкрийте `http://localhost:8000/login`
2. Введіть облікові дані:
   - Email: `admin@example.com`
   - Password: `admin123`
3. Натисніть "Sign in"
4. Повинно перенаправити на `/admin`

**Тест виходу:**
1. Перейдіть на `http://localhost:8000/logout`
2. Повинно перенаправити на сторінку входу

### 4. Тестування ролей та прав доступу

**Тест 1: Доступ адміністратора**
- Увійдіть як `admin@example.com` (пароль: `admin123`)
- Відкрийте `/admin`
- Повинен бути доступ до всіх функцій

**Тест 2: Доступ звичайного користувача**
- Увійдіть як `user@example.com` (пароль: `user123`)
- Спробуйте відкрити `/admin`
- Повинна з'явитися помилка доступу (403 Forbidden) якщо налаштовано `ROLE_ADMIN`

### 5. Перевірка без браузера (через curl)

**Перевірка головної сторінки:**
```bash
curl -I http://localhost:8000
```

**Очікуваний результат:**
```
HTTP/1.1 200 OK
або
HTTP/1.1 404 Not Found
```

**Перевірка адмін-панелі:**
```bash
curl http://localhost:8000/admin
```

### 6. Додаткові корисні команди для тестування

**Перевірка конфігурації:**
```bash
# Перевірка налаштувань Doctrine
php bin/console doctrine:mapping:info

# Перевірка підключення до БД
php bin/console doctrine:query:sql "SELECT 1"

# Перевірка security налаштувань
php bin/console debug:firewall

# Список всіх сервісів
php bin/console debug:container
```

**Перевірка валідності конфігурації:**
```bash
# Перевірка YAML синтаксису
php bin/console lint:yaml config/

# Перевірка Twig шаблонів
php bin/console lint:twig templates/

# Перевірка контейнера
php bin/console lint:container
```

---

## Корисні команди Symfony

### Загальні команди

```bash
# Список всіх доступних команд
php bin/console list

# Допомога по конкретній команді
php bin/console help [command]

# Інформація про середовище
php bin/console about
```

### Doctrine команди

```bash
# Створити базу даних
php bin/console doctrine:database:create

# Видалити базу даних
php bin/console doctrine:database:drop --force

# Створити міграцію
php bin/console make:migration

# Виконати міграції
php bin/console doctrine:migrations:migrate

# Відкатити останню міграцію
php bin/console doctrine:migrations:migrate prev

# Статус міграцій
php bin/console doctrine:migrations:status

# Завантажити fixtures
php bin/console doctrine:fixtures:load

# SQL запит
php bin/console doctrine:query:sql "SELECT * FROM user"
```

### Генерація коду (Maker Bundle)

```bash
# Створити контролер
php bin/console make:controller

# Створити сутність
php bin/console make:entity

# Створити форму
php bin/console make:form

# Створити CRUD
php bin/console make:crud

# Створити fixtures
php bin/console make:fixtures

# Створити автентифікацію
php bin/console make:auth

# Створити user
php bin/console make:user
```

---

## Можливі проблеми та рішення

### Помилка підключення до БД

**Симптом:** `Connection refused` або `Access denied`

**Рішення:**
1. Перевірте, чи запущений MySQL/MariaDB
2. Перевірте правильність даних у `.env`
3. Перевірте пароль та права користувача БД:
```bash
mysql -u root -p
```

```sql
GRANT ALL PRIVILEGES ON symfony_admin_lab.* TO 'root'@'localhost';
FLUSH PRIVILEGES;
```

### Помилка кешу

**Симптом:** Зміни не відображаються

**Рішення:**
```bash
php bin/console cache:clear
rm -rf var/cache/*
```

### Помилка прав доступу

**Симптом:** `Permission denied` при записі

**Рішення (Linux/Mac):**
```bash
chmod -R 777 var/
chmod -R 777 public/bundles/
```

---

## Додаткові ресурси

- Офіційна документація Symfony: https://symfony.com/doc/current/index.html
- Документація EasyAdmin: https://symfony.com/bundles/EasyAdminBundle/current/index.html
- Документація Doctrine: https://www.doctrine-project.org/
- Symfony Cast: https://symfonycasts.com/

---

## Ліцензія

Проєкт створено для навчальних цілей.

Repository: https://github.com/sergiyscherbakov/symfony-easyadmin-project
