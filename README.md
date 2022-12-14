# yamdb_final
![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![Django](https://img.shields.io/badge/django-%23092E20.svg?style=for-the-badge&logo=django&logoColor=white)
![Postgres](https://img.shields.io/badge/postgres-%23316192.svg?style=for-the-badge&logo=postgresql&logoColor=white)<br/>
![yamdb workflow](https://github.com/zerg959/yamdb_final/workflows/yamdb_workflow/badge.svg)
<br/>


test server deployed on 84.252.142.54<br/>
login page: http://84.252.142.54/admin/</br>
documentation: http://84.252.142.54/redoc/

### Описание: ###
API для социальной сети Yatube, где пользователи могут регистрироваться и оставлять свои отзывы.

Произведения делятся на категории: «Книги», «Фильмы», «Музыка» (возможно расширение списка админом).

Сами произведения в проекте не хранятся, здесь нельзя посмотреть фильм или послушать музыку.

В каждой категории есть произведения: книги, фильмы или музыка. Например, в категории «Книги» могут быть произведения «Винни-Пух и все-все-все» и «Марсианские хроники», а в категории «Музыка» — песня «Давеча» группы «Насекомые» и вторая сюита Баха.

Произведению может быть присвоен жанр «Сказка», «Рок» или «Артхаус» (возможно расширение списка админом).

 Благодарные или возмущённые пользователи оставляют к произведениям текстовые отзывы и ставят произведению оценку в диапазоне от одного до десяти; из пользовательских оценок формируется усреднённая оценка произведения — рейтинг. На одно произведение пользователь может оставить только один отзыв.

## Установка: ##

### Клонируйте репозиторий: ###

    git clone git@github.com:zerg959/yamdb_final_latest.git


### Пример файла `.env`. Должен находится в папке `./api_yamdb/infra/`: ###

    SECRET_KEY=... (ключ к Джанго проекту)
    DB_ENGINE=django.db.backends.postgresql (указываем, что работаем с postgresql)
    DB_NAME=postgres (имя базы данных)
    POSTGRES_USER=... (логин для подключения к базе данных)
    POSTGRES_PASSWORD=... (пароль для подключения к БД (установите свой)
    DB_HOST=db (название сервиса (контейнера)
    DB_PORT=5432 (порт для подключения к БД)

### Перейдите в репозиторий к директории с файлом docker-compose.yaml с помощью командной строки: ###

    cd yamdb_final_latest/api_yamdb/infra/
  
### Установите [Docker и Docker-compose](https://docs.docker.com/engine/install/ubuntu/). Запустите сборку образов: ###

    sudo docker-compose up

### или

    sudo docker-compose up -d --build
  
### После развертывания проекта создайте миграции и заполнените базу данных: ###

    sudo docker-compose exec python manage.py migrate
    sudo docker-compose exec python manage.py createsuperuser
    sudo docker-compose exec python manage.py collectstatic

## Алгоритм регистрации пользователей ##
  
1. Пользователь отправляет POST-запрос на добавление нового пользователя с параметрами `email` и `username` на эндпоинт `/api/v1/auth/signup/`.  
2. YaMDB отправляет письмо с кодом подтверждения `confirmation_code` на адрес `email`. В проекте реализован бэкенд почтового сервиса, папка - `sent_emails`.  

3. Пользователь отправляет POST-запрос с параметрами `username` и `confirmation_code` на эндпоинт `/api/v1/auth/token/`, в ответе на запрос ему приходит token (JWT-токен).  
4. При желании пользователь отправляет PATCH-запрос на эндпоинт `/api/v1/users/me/` и заполняет поля в своём профайле.  

### ReDoc:

    http://127.0.0.1:8000/redoc/

## Автор:
Лукичев Илья (https://github.com/zerg959)

