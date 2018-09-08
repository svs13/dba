## Домашнее задание:
	
## 1 Создайте в MySQL, Postgres и SQLite одинаковые базы данных:

#### MySQL
	CREATE DATABASE `dba1`;
#### PostgreSQL
	CREATE DATABASE "dba1";
#### SQLite
через ide создал файл-базу данных dba1.sqlite

Сделано

## 1.1 Изучите понятие типа SERIAL в разных базах данных.
## Подсказка - в SQLite такого типа нет, но есть модификатор типа AUTOINCREMENT.

#### MySQL
тип SERIAL - это alias/псевдоним,  соответствует типу BIGINT UNSIGNED NOT NULL AUTO_INCREMENT UNIQUE
#### PostgreSQL
тип SERIAL - это числовой тип: serial	4 bytes	autoincrementing integer	1 to 2147483647
#### SQLite
типа SERIAL нет. Для реализации автоинкремента достаточно задавать INTEGER PRIMARY KEY.
При наличии AUTOINCREMENT, когда одно из полей имеет значения верхнего предела (9223372036854775807) при инкременте - будет ошибка.
Если не дописывать AUTOINCREMENT, то будут заполняться все не использованные значения.

## 1.2 Таблица books, содержащая, как минимум, информацию о заглавии книги, годе выхода, авторе и цене.
## И конечно же, серийный номер записи в таблице (см. выше п. 1.1). Дополнительные поля - по желанию.

#### MySQL
	CREATE TABLE `books` (`id` SERIAL, `title` VARCHAR(100), `year` SMALLINT, `author` VARCHAR(100), `price` DECIMAL(8,2));
#### PostgreSQL
	CREATE TABLE "books" ("id" SERIAL, "title" VARCHAR(100), "year" SMALLINT, "author" VARCHAR(100), "price" DECIMAL(8,2));
#### SQLite
	CREATE TABLE `books` (`id` INTEGER PRIMARY KEY AUTOINCREMENT, `title` VARCHAR(100), `year` SMALLINT, `author` VARCHAR(100), `price` DECIMAL(8,2));

## 1.3 Таблица publishers, содержащая информацию об издательствах. 
## Поля - на ваш вкус, за исключением серийного номера.

#### MySQL
	CREATE TABLE `publishers` (`id` SERIAL, `name` VARCHAR(50), `full_name` VARCHAR(100), `city` VARCHAR(50), `isbn` VARCHAR(30));
#### PostgreSQL
	CREATE TABLE "publishers" ("id" SERIAL, "name" VARCHAR(50), "full_name" VARCHAR(100), "city" VARCHAR(50), "isbn" VARCHAR(30));
#### SQLite
	CREATE TABLE `publishers` (`id` INTEGER PRIMARY KEY AUTOINCREMENT, `name` VARCHAR(50), `full_name` VARCHAR(100), `city` VARCHAR(50), `isbn` VARCHAR(30));

## 2 Наполните таблицы произвольными данными.

#### MySQL, SQLite
	INSERT INTO `books` (`title`, `year`, `author`, `price`) VALUES ('Название 1', '1900', 'Автор 1', '100.00');
	INSERT INTO `books` (`title`, `year`, `author`, `price`) VALUES ('Название 2', '1800', 'Автор 2', '500.00');
	INSERT INTO `books` (`title`, `year`, `author`, `price`) VALUES ('Название 3', '2000', 'Автор 3', '1000.00');
	INSERT INTO `books` (`title`, `year`, `author`, `price`) VALUES ('Название 4', '2018', 'Автор 4', '1500.00');
	INSERT INTO `books` (`title`, `year`, `author`, `price`) VALUES ('Название 5', '1888', 'Автор 5', '2000.00');
	INSERT INTO `publishers` (`name`, `full_name`, `city`, `isbn`) VALUES ('Изд 1', 'Издательство 1', 'Город 1', '978-5-354');
	INSERT INTO `publishers` (`name`, `full_name`, `city`, `isbn`) VALUES ('Изд 2', 'Издательство 2', 'Город 2', '978-5-355');
	INSERT INTO `publishers` (`name`, `full_name`, `city`, `isbn`) VALUES ('Изд 3', 'Издательство 3', 'Город 3', '978-5-356');
#### PostgreSQL
	INSERT INTO "books" ("title", "year", "author", "price") VALUES ('Название 1', '1900', 'Автор 1', '100.00');
	INSERT INTO "books" ("title", "year", "author", "price") VALUES ('Название 2', '1800', 'Автор 2', '500.00');
	INSERT INTO "books" ("title", "year", "author", "price") VALUES ('Название 3', '2000', 'Автор 3', '1000.00');
	INSERT INTO "books" ("title", "year", "author", "price") VALUES ('Название 4', '2018', 'Автор 4', '1500.00');
	INSERT INTO "books" ("title", "year", "author", "price") VALUES ('Название 5', '1888', 'Автор 5', '2000.00');
	INSERT INTO "publishers" ("name", "full_name", "city", "isbn") VALUES ('Изд 1', 'Издательство 1', 'Город 1', '978-5-354');
	INSERT INTO "publishers" ("name", "full_name", "city", "isbn") VALUES ('Изд 2', 'Издательство 2', 'Город 2', '978-5-355');
	INSERT INTO "publishers" ("name", "full_name", "city", "isbn") VALUES ('Изд 3', 'Издательство 3', 'Город 3', '978-5-356');


## 3 Создайте запросы, выбирающие:
## 3.1 Все книги определенного автора

#### MySQL, SQLite
	SELECT * FROM `books` WHERE `author`='Автор 2';
#### PostgreSQL
	SELECT * FROM "books" WHERE "author"='Автор 2';

## 3.2 Все книги ценой не более 500 рублей

#### MySQL, SQLite
	SELECT * FROM `books` WHERE `price`<='500.00';
#### PostgreSQL
	SELECT * FROM "books" WHERE "price"<='500.00';

## 3.3 Заглавия книг (и год издания) определенного автора, отсортированные по году их издания

#### MySQL, SQLite
	SELECT `title`, `year` FROM `books` WHERE `author`='Автор 2' ORDER BY `year`;
#### PostgreSQL
	SELECT "title", "year" FROM "books" WHERE "author"='Автор 2' ORDER BY "year";

## 3.4 Имена авторов книг, вышедших в 1990-е годы

#### MySQL, SQLite
	SELECT `author` FROM `books` WHERE `year` BETWEEN '1990' AND '1999';
#### PostgreSQL
	SELECT "author" FROM "books" WHERE "year" BETWEEN '1990' AND '1999';

## 4 Для каждой БД запросы, которые вы использовали в пунктах выше, запишите в отдельный текстовый файл.
## Приложите текстовый файл с пояснениями к пункту 1.1. 
## Все файлы упакуйте в архив ZIP и приложите, как домашнее задание.

Сделано. По согласованию - текстовый файл загружен на гитхаб.
