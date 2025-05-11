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
>-p 5432:5432  \
>postgres:14
![image](https://github.com/user-attachments/assets/85d54ce9-9f7a-43de-9a62-5a053100ed03)


проверка версии

![image](https://github.com/user-attachments/assets/bcddf793-f9ac-4104-b08e-96066efafdf0)
![image](https://github.com/user-attachments/assets/d38a39c5-d706-4a4c-822b-2f6bfb10e264)

проверка /var/lib/postgres, локально на VM директория содержит данные от Postgres базы в Docker
![image](https://github.com/user-attachments/assets/b746756b-6fb8-439f-8b98-495941cf6acf)




## (5) Разверните контейнер с клиентом PostgreSQL. ##
В [PostgreSQL Docker client-only Image](https://datmt.com/backend/quering-postgresql-with-docker/) нашел образ(image) включающий в себя только psql(клиент)

выполнил установку
>docker run -dit --network=db --name=pgclient codingpuss/postgres-client
![image](https://github.com/user-attachments/assets/88c022fa-683c-4d61-96e9-6babd5fad9a2)

проверка подключения
>docker exec -it pgclient psql postgresql://postgres:5af45Q4ae3Xa3Ff4@pgserver:5432/postgres -c 'select inet_server_addr();'
![image](https://github.com/user-attachments/assets/ce6bb8d6-0bdd-406c-b214-3f489a0ae021)

Как альтернативный вариант, можно было поднять контрейнер с голой UBUNTU и установить там клиента через
>sudo apt-get install -y postgresql-client
Решил попробовать более сложный путь. 


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

Выполнил создание таблицы и вставку из под клиента
![image](https://github.com/user-attachments/assets/55cbcb64-0d03-495b-82ed-a09d52a50381)

проверка из PGCLIENT
![image](https://github.com/user-attachments/assets/8a10f20f-1a16-488d-89df-5b1eb6f8e985)


проверка из PGSERVER
>docker exec -it pgserver bash
![image](https://github.com/user-attachments/assets/1f89a306-e715-4566-b84a-c26e1c2b7f27)

   
## (7) Подключитесь к контейнеру с сервером с ноутбука или компьютера. ##
Подключился успешно
![image](https://github.com/user-attachments/assets/0938f8a0-809f-4c38-9382-a72313a9eadf)
![image](https://github.com/user-attachments/assets/4321c004-3b77-45c9-9ee6-6cd7b07d7e70)


## (8) Удалите контейнер с сервером и создайте его заново. ##
Удалил контейнер pgserver
![image](https://github.com/user-attachments/assets/b731f7af-d344-4bfd-b3ee-9f3e59aaccb6)

Пересоздал его
>docker container run \
>--name pgserver \
>--network db \
>-e POSTGRES_PASSWORD=5af45Q4ae3Xa3Ff4 \
>-e PGDATA=/var/lib/postgres/pgdata \
>-v /var/lib/postgres:/var/lib/postgres \
>-p 5432:5432  \
>postgres:14
![image](https://github.com/user-attachments/assets/135055d0-968c-418a-9b9e-6d7b32f7f790)


## (9) Проверьте, что данные остались на месте. ##
Данные на месте
![image](https://github.com/user-attachments/assets/40414785-c68c-450d-8e09-c78b1a3be61b)

