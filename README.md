## Яндекс-Проект Foodgram

«Фудграм»: сайт, на котором пользователи публикуют рецепты, подписываются на публикации других авторов и добавляют рецепты в избранное. Сервис «Список покупок» позволит пользователю создавать список продуктов, которые нужно купить для приготовления выбранных блюд.


В документации описаны возможные запросы к API и структура ожидаемых ответов. Для каждого запроса указаны уровни прав доступа.

### Технологии:

Python, Django, Django Rest Framework, Docker, Gunicorn, NGINX, PostgreSQL, Yandex Cloud, Continuous Integration, Continuous Deployment

### Развернуть проект на удаленном сервере:

- Клонировать репозиторий:
```
https://github.com/nansysh/foodgram.git
```

- Установить на сервере Docker, Docker Compose:

```
sudo apt install curl                                   # установка утилиты для скачивания файлов
curl -fsSL https://get.docker.com -o get-docker.sh      # скачать скрипт для установки
sh get-docker.sh                                        # запуск скрипта
sudo apt-get install docker-compose-plugin              # последняя версия docker compose
```

- Скопировать на сервер файлы docker-compose.production.yml, nginx.conf из папки infra (команды выполнять находясь в папке infra):

```
scp docker-compose.production.yml nginx.conf username@IP:/home/username/   # username - имя пользователя на сервере
                                                                # IP - публичный IP сервера
```


- Создать и запустить контейнеры Docker, выполнить команду на сервере
```
sudo docker compose up -d
```

- После успешной сборки выполнить миграции:
```
sudo docker compose exec backend python manage.py migrate
```

- Создать суперпользователя:
```
sudo docker compose exec backend python manage.py createsuperuser
```

- Собрать статику:
```
sudo docker compose exec backend python manage.py collectstatic
```

- Для остановки контейнеров Docker:
```
sudo docker compose down -v      # с их удалением
sudo docker compose stop         # без удаления
```

- Наполнить базу данных содержимым из файла ingredients.json в admin-зоне сайта:
```
http://<your IP>/admin/recipes/ingredient/

Данные для доступа:
login: admin
password: 1
Файл для загрузки ингредиентов:
foodgram-project-react/backend/data/ingredients.json
```
### Запуск проекта на локальной машине:

- Клонировать репозиторий:
```
https://github.com/nansysh/foodgram-project-react.git
```

- В директории infra файл .env.db переименовать в .env и заполнить своими данными:
```
DB_ENGINE=django.db.backends.postgresql
DB_NAME=postgres
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
DB_HOST=db
DB_PORT=5432
SECRET_KEY='секретный ключ Django'
```

- Создать и запустить контейнеры Docker, как указано выше.


- После запуска проект будут доступен по адресу: [http://localhost/](http://localhost/)


- Документация будет доступна по адресу: [http://localhost/api/docs/](http://localhost/api/docs/)


### Автор:

Анастасия nansysh 
