# Домашнее Задание Евгения Сартисона #



## (1) Создайте инстанс с Ubuntu 20.04 в Яндекс.Облаке или аналогах. ##


## (2) Установите Docker Engine. ##


## (3) Создайте каталог /var/lib/postgres для хранения данных. ##


## (4) Разверните контейнер с PostgreSQL 14, смонтировав в него /var/lib/postgres. ##


## (5) Разверните контейнер с клиентом PostgreSQL. ##

## (6) Подключитесь из контейнера с клиентом к контейнеру с сервером и создайте таблицу с данными о перевозках. ##

  >sql
  >create table shipments(id serial, product_name text, quantity int, destination text);
   
   >insert into shipments(product_name, quantity, destination) values('bananas', 1000, 'Europe');
   >insert into shipments(product_name, quantity, destination) values('bananas', 1500, 'Asia');
   >insert into shipments(product_name, quantity, destination) values('bananas', 2000, 'Africa');
   >insert into shipments(product_name, quantity, destination) values('coffee', 500, 'USA');
   >insert into shipments(product_name, quantity, destination) values('coffee', 700, 'Canada');
   >insert into shipments(product_name, quantity, destination) values('coffee', 300, 'Japan');
   >insert into shipments(product_name, quantity, destination) values('sugar', 1000, 'Europe');
   >insert into shipments(product_name, quantity, destination) values('sugar', 800, 'Asia');
   >insert into shipments(product_name, quantity, destination) values('sugar', 600, 'Africa');
   >insert into shipments(product_name, quantity, destination) values('sugar', 400, 'USA');
   
## (7) Подключитесь к контейнеру с сервером с ноутбука или компьютера. ##


## (8) Удалите контейнер с сервером и создайте его заново. ##

## (9) Проверьте, что данные остались на месте. ##
