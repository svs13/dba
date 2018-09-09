Домашнее задание:
-----------------
    
1 Спроектируйте таблицу для хранения товаров. У каждого товара есть:
--------------------------------------------------------------------
## 1.1 Наименование
## 1.2 Артикул (внутренний код)
## 1.3 Изображение (разумно хранить его URL)
## 1.4 Цена
## 1.5 Дата появления в продаже
## 1.6 Количество на складе
## 1.7 Другие поля - на ваш вкус


#### MySQL
полям price и quantity задаю тип - только положительное значение UNSIGNED
полю vendor_code задаю тип - уникальное значение UNIQUE
поле vendor_code - это внутренний код. Кол-во разновидностей товаров задаю не более 999 999 999.
в поле vendor_code допускаю использование не числовых символов

    CREATE TABLE `products` (
      `id` SERIAL,
      `name` VARCHAR(100),
      `vendor_code` CHAR(9) UNIQUE,
      `image` VARCHAR(100),
      `price` DECIMAL(8,2) UNSIGNED,
      `sale_date` DATE,
      `quantity` INT UNSIGNED
    );


#### PostgreSQL
здесь нет модификатора UNSIGNED, использую ограничение CHECK (VALUE >= 0)
так же здесь SERIAL может быть неуникальным (при ручном вводе) - задаю уникальным UNIQUE

    CREATE TABLE "products" (
      "id" SERIAL UNIQUE,
      "name" VARCHAR(100),
      "vendor_code" CHAR(9) UNIQUE,
      "image" VARCHAR(100),
      "price" NUMERIC(8,2) CHECK ("price" >= 0),
      "sale_date" DATE,
      "quantity" INTEGER CHECK ("quantity" >= 0)
    );

#### SQLite
список возможных ограничений: NOT NULL, CHECK, UNIQUE, PRIMARY KEY and FOREIGN KEY
Здесь нет типа SERIAL, создаю его модификаторами из числа. INTEGER PRIMARY KEY AUTOINCREMENT
Здесь нет типа DATE вместо него, по документации, предлагается использовать ф-и даты и времени. 
Выбираю формат хранения времени - ISO8601, как более удобный для представления. Для этого подходит тип TEXT
пару примеров возвращающих данные в формате ISO8601:
- date('now', 'locale') - получение текущей локальной даты в ISO8601
- date('2015-11-11') или писать ручками '2015-11-11'

    CREATE TABLE `products` (
      `id` INTEGER PRIMARY KEY AUTOINCREMENT,
      `name` TEXT,
      `vendor_code` TEXT UNIQUE,
      `image` TEXT,
      `price` REAL CHECK (`price` >= 0),
      `sale_date` TEXT,
      `quantity` INTEGER CHECK (`quantity` >= 0)
    );

2 Заполните эту таблицу данными - внесите в нее 4-5 товаров 
-----------------------------------------------------------

#### MySQL
    INSERT INTO `products` (`name`, `vendor_code`, `image`, `price`, `sale_date`, `quantity`)
        VALUES ('Название 1', '123456', 'image 1.jpg', '100.00', '2018-10-15', 42);
    INSERT INTO `products` (`name`, `vendor_code`, `image`, `price`, `sale_date`, `quantity`)
        VALUES ('Название 2', '222222', 'image 2.jpg', '150.00', '2018-09-25', 33);
    INSERT INTO `products` (`name`, `vendor_code`, `image`, `price`, `sale_date`, `quantity`)
        VALUES ('Название 3', '000001', 'image 3.jpg', '333.00', '2018-11-11', 11);
    INSERT INTO `products` (`name`, `vendor_code`, `image`, `price`, `sale_date`, `quantity`)
        VALUES ('Название 4', '100001', 'image 4.jpg', '9999.00', '2018-09-09', 9999);
    SELECT * FROM `products`;
поле vendor_code пробелами не добилось до 9 символов '123456'

#### PostgreSQL
    INSERT INTO "products" ("name", "vendor_code", "image", "price", "sale_date", "quantity") VALUES 
        ('Название 1', '123456', 'image 1.jpg', '100.00', '2018-10-15', 42),
        ('Название 2', '222222', 'image 2.jpg', '150.00', '2018-09-25', 33),
        ('Название 3', '000001', 'image 3.jpg', '333.00', '2018-11-11', 11),
        ('Название 4', '100001', 'image 4.jpg', '9999.00', '2018-09-09', 9999);
    SELECT * FROM "products";
!!! поле vendor_code ДОБИЛОСЬ ПРОБЕЛАМИ СПРАВА до 9 символов '123456   ' , да, помню - тоже на уроке сказано и в слайдах написано.

#### SQLite
    INSERT INTO `products` (`name`, `vendor_code`, `image`, `price`, `sale_date`, `quantity`) VALUES 
        ('Название 1', '123456', 'image 1.jpg', '100.00', '2018-10-15', 42),
        ('Название 2', '222222', 'image 2.jpg', '150.00', '2018-09-25', 33),
        ('Название 3', '000001', 'image 3.jpg', '333.00', '2018-11-11', 11),
        ('Название 4', '100001', 'image 4.jpg', '9999.00', '2018-09-09', 9999);
    SELECT * FROM `products`;
поле vendor_code пробелами не добилось до 9 символов '123456'

    
3 Поэкспериментируйте со вставкой некорректных данных (отрицательная цена? количество на складе менее нуля? пустой артикул?). 
-----------------------------------------------------------------------------------------------------------------------------
Запишите, как реагирует БД на такие попытки (в отдельный текстовый файл)
-----------------------------------------------------------------------------------------------------------------------------

#### MySQL
см. 'mysqlIncorrectData.txt'
#### PostgreSQL
см. 'postgresqlIncorrectData.txt'
#### SQLite
см. 'sqliteIncorrectData.txt'


Выполните задание в трех базах данных. Запишите ВСЕ запросы, которые вы использовали.
-------------------------------------------------------------------------------------
Эти запросы и письменный отчет о попытках вставки некорректных данных и будут ваших домашним заданием.

Сделано. Узнал много чего нового =)
