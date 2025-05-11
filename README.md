# Домашнее Задание Евгения Сартисона #



## (1) Создайте инстанс с Ubuntu 20.04 в Яндекс.Облаке или аналогах. ##
В YC создал VM под управлением Ubuntu 20.04
![image](https://github.com/user-attachments/assets/e85a0ef2-c775-46fc-8922-1e1f72fefe61)


## (2) Установите Docker Engine. ##
Выполнил инсталляцию Docker Engine по официальному документу [Install using the apt repository](https://docs.docker.com/engine/install/ubuntu/)
![image](https://github.com/user-attachments/assets/23e4edf9-764e-4a77-84cb-e7c8c5b94747)

Проверка Docker-а прошла успешно

![image](https://github.com/user-attachments/assets/4f512a63-3628-490c-8ae5-9215f493093b)



## (3) Создайте каталог /var/lib/postgres для хранения данных. ##
![image](https://github.com/user-attachments/assets/27d4c310-ce5c-4917-a989-76756838a9ae)



## (4) Разверните контейнер с PostgreSQL 14, смонтировав в него /var/lib/postgres. ##

создадим сеть, так-как потребуется взаимодействие с контейнером для pg клиента
![image](https://github.com/user-attachments/assets/a5155ca2-6266-4640-92f7-9de98d5cb7cd)

Запустим сам контейнер
>docker container run \
>--name pgserver \
>--network db \
>-e POSTGRES_PASSWORD=5af45Q4ae3Xa3Ff4 \
>-e PGDATA=/var/lib/postgres/pgdata \
>-v /var/lib/postgres:/var/lib/postgres \
>postgres:14
![image](https://github.com/user-attachments/assets/85d54ce9-9f7a-43de-9a62-5a053100ed03)


проверка версии

![image](https://github.com/user-attachments/assets/bcddf793-f9ac-4104-b08e-96066efafdf0)
![image](https://github.com/user-attachments/assets/d38a39c5-d706-4a4c-822b-2f6bfb10e264)

проверка /var/lib/postgres, локально на VM директория содержит данные от Postgres базы в Docker
![image](https://github.com/user-attachments/assets/b746756b-6fb8-439f-8b98-495941cf6acf)




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
