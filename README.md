# API сервиса YaMDb

![yamdb_workflow](https://github.com/KceHNa/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)
![](https://img.shields.io/badge/Python-3.7.5-blue) 
![](https://img.shields.io/badge/Django-2.2.16-green)
![](https://img.shields.io/badge/DjangoRestFramework-3.12.4-red)
![](https://img.shields.io/badge/Docker-3.8-yellow)
 <br> <br>

### Описание. 
Сервер доступен по адресу --> http://84.201.178.226/
Проект YaMDb собирает отзывы пользователей на произведения. Произведения делятся на категории: «Книги», «Фильмы», «Музыка».

**Возможности:**

:black_small_square: Регистрация на сайте, получение токена, изменение данных своей учетной записи<br>
:black_small_square: Раздаление прав пользователей согласно, назначенной ему роли<br>
:black_small_square: Возможность, согласно авторизации выполнять следующие дествия: получать, добавлять и удалять - категорию, жанр, произведение, отзыв и комментарий<br>
:black_small_square: Администрирование пользователями<br><br>

### Как запустить проект.

Клонировать репозиторий и перейти в него в командной строке:

```
git clone <название_проекта_в_git>.git
cd <название_проекта_в_git>
```

Создайте файл .env из дефолтного .env.default

Запустите Docker
```
docker-compose up
```
Или при пересборке без логов
```
docker-compose up -d --build 
```

Выполнить миграции, создать суперпользователя и собрать статику:
```
docker-compose exec web python manage.py migrate
docker-compose exec web python manage.py createsuperuser
docker-compose exec web python manage.py collectstatic --no-input
```
Готово! Админка --> http://84.201.178.226/admin

Остановить проект:
```
docker-compose down -v 
```

### Документация к API

Доступна по адресу http://84.201.178.226/redoc/ . Здесь можно увидеть все возможные запросы к api и ответы.

### Ресурсы API YaMDb

* auth: аутентификация.
* users: пользователи.
* titles: произведения, к которым пишут отзывы (определённый фильм, книга или песенка).
* categories: категории (типы) произведений («Фильмы», «Книги», «Музыка»).
* genres: жанры произведений. Одно произведение может быть привязано к нескольким жанрам.
* reviews: отзывы на произведения. Отзыв привязан к определённому произведению.
* comments: комментарии к отзывам. Комментарий привязан к определённому отзыву.

### Пример работы API:

Запрос для создания поста:
```python
from pprint import pprint

import requests

url = 'http://127.0.0.1/api/v1/categories/'
request = requests.get(url).json()
pprint(request)
```
Ответ от API:
```json
{"count": 3,
 "next": "None",
 "previous": "None",
 "results": [{"name": "Фильм", "slug": "movie"},
             {"name": "Книга", "slug": "book"},
             {"name": "Музыка", "slug": "music"}]}
```
---
### Дополнительные команды

Запуск теста в виртуальном окружении
```
python3 -m venv venv
source venv/bin/activate
python3 -m pip install --upgrade pip
pip install -r requirements.txt
python -m pytest tests/
```

Дамп базы
```
docker-compose exec web python manage.py dumpdata > fixtures.json 
```
---

### Автор
Ксения Фурсова @kcehna
