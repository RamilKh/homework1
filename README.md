# Курс БД. Домашнее задание №1
## Проектирование дипломного проекта «Он-лайн встреч(конференций)»

## Схема
![](entities.png?raw=true)



## Документация
Приложение для проведения быстрых он-лайн встреч(конференций).


## Сущности

Таблица Users. Пользователи системы.
| Название       | Тип                      | Ключ  | Комментарий              |
| -------------- |--------------------------| ------|--------------------------|
| pk             | int                      | PK    |                          |
| first_name     | character varying(100)   | -     | Имя                      |
| last_name      | character varying(100)   | -     | Фамилия                  |
| email          | character varying(100)   | -     | E-mail                   |
| password       | character varying(255)   | -     | Пароль                   |
| online         | boolean                  | -     | Находиться ли в системе  |



Таблица UsersInfo. Дополнительная информация по пользователям системы.
| Название       | Тип                      | Ключ  | Комментарий              |
| -------------- |--------------------------| ------|--------------------------|
| pk             | int                      | PK    |                          |
| image          | character varying(255)   | -     | Фото                     |
| url_www        | character varying(200)   | -     | Ссылка на личный сайт    |
| url_social     | character varying(200)   | -     | Ссылка на соцсеть        |



Таблица Teams. Команды.
| Название       | Тип                      | Ключ  | Комментарий              |
| -------------- |--------------------------| ------|--------------------------|
| pk             | int                      | PK    |                          |
| pk_user        | int                      | FK    | Чья команда. PK Users    |
| name           | character varying(255)   | -     | Название                 |



Таблица TeamsUser. Связка пользователей и команд.
| Название       | Тип                      | Ключ  | Комментарий              |
| -------------- |--------------------------| ------|--------------------------|
| pk             | int                      | PK    |                          |
| pk_team        | int                      | FK    | PK Teams                 |
| pk_user        | int                      | FK    | PK Users                 |



Таблица Meetings. Встречи (лекции, online конференции и т.п)
| Название       | Тип                      | Ключ  | Комментарий                 |
| -------------- |--------------------------| ------|-----------------------------|
| pk             | int                      | PK    |                             |
| name           | character varying(100)   | -     | Название                    |
| status         | smallint                 | -     | Статус(завершен/проводится) |
| created_at     | timestamp                | -     | Дата создания               |
| start_dt       | timestamp                | -     | Когда начнется              |



Таблица Tasks. Задачи к Meetings.
| Название       | Тип                      | Ключ  | Комментарий                 |
| -------------- |--------------------------| ------|-----------------------------|
| pk             | int                      | PK    |                             |
| pk_meeting     | int                      | FK    | PK Meetings                 |
| name           | character varying(255)   | -     | Название                    |
| content        | text                     | -     | Содержание/текст            |



Таблица Docs. Материалы к Meetings.
| Название       | Тип                      | Ключ  | Комментарий                 |
| -------------- |--------------------------| ------|-----------------------------|
| pk             | int                      | PK    |                             |
| pk_meeting     | int                      | FK    | PK Meetings                 |
| name           | character varying(255)   | -     | Название                    |
| filename       | character varying(255)   | -     | Файл                        |



Таблица Members. Участники Meetings.
| Название       | Тип                      | Ключ  | Комментарий                 |
| -------------- |--------------------------| ------|-----------------------------|
| pk             | int                      | PK    |                             |
| pk_meeting     | int                      | FK    | PK Meetings                 |
| pk_user        | int                      | FK    | PK Users                    |



Таблица Reports. Отчет к Meetings.
| Название       | Тип                      | Ключ  | Комментарий                 |
| -------------- |--------------------------| ------|-----------------------------|
| pk             | int                      | PK    |                             |
| pk_meeting     | int                      | FK    | PK Meetings                 |
| users_visit    | json                     | -     | Какие пользователи посетили |
| content        | text                     | -     | Содержание/текст            |



Таблица Posts. Чат в Meetings.
| Название       | Тип                      | Ключ  | Комментарий                 |
| -------------- |--------------------------| ------|-----------------------------|
| pk             | int                      | PK    |                             |
| pk_meeting     | int                      | FK    | PK Meetings                 |
| pk_user        | int                      | FK    | PK Users                    |
| content        | text                     | -     | Текст                       |


## Примеры бизнес-задач которые решает база
- Управление встречами.
- Создание отчетов по встречам.
- Загрузка материалов к встречам.
- Управление пользователями.
- Отправка сообщений в чат встречи.
- Добавление/удаление участников встречи.
