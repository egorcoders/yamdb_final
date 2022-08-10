# Проект YaMDb

![example workflow](https://github.com/egorcoders/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)
[![Python](https://img.shields.io/badge/-Python-464641?style=flat-square&logo=Python)](https://www.python.org/)
[![pytest](https://img.shields.io/badge/-pytest-464646?style=flat-square&logo=pytest)](https://docs.pytest.org/en/6.2.x/)
[![Django](https://img.shields.io/badge/-Django-464646?style=flat-square&logo=Django)](https://www.djangoproject.com/)

Яндекс Практикум. Проект 16-го спринта: CI и CD проекта api_yamdb.

## Описание

Проект **YaMDb** собирает отзывы пользователей на произведения из категорий: «Книги», «Фильмы», «Музыка».

## Функционал

- Произведения делятся на категории: «Книги», «Фильмы», «Музыка». Список категорий может быть расширен администратором;
- Сами произведения в YaMDb не хранятся, здесь нельзя посмотреть фильм или послушать музыку;
- В каждой категории есть произведения: книги, фильмы или музыка. Например, в категории «Книги» могут быть произведения «Винни-Пух и все-все-все» и «Марсианские хроники», а в категории «Музыка» — песня «Давеча» группы «Насекомые» и вторая сюита Баха;
- Произведению может быть присвоен жанр из списка предустановленных. Новые жанры может создавать только администратор;
- Благодарные или возмущённые пользователи оставляют к произведениям текстовые отзывы и ставят произведению оценку в диапазоне от одного до десяти; из пользовательских оценок формируется усреднённая оценка произведения — рейтинг. На одно произведение пользователь может оставить только один отзыв.

## Установка

Клонировать репозиторий:

```python
git clone https://github.com/egorcoders/yamdb_final.git
```

Создать `.env` файл на уровне с файлом `docker-compose.yaml` в директории infra с указаниме данных:

- SECRET_KEY - секретный ключ Django;
- DB_ENGINE - движок базы данных (БД) postgresql: `django.db.backends.postgresql`;
- DB_NAME - имя БД: `postgres`;
- POSTGRES_USER - пользователь БД: `postgres`;
- POSTGRES_PASSWORD - пароль рользователя БД: `postgres`;
- DB_HOST - адрес удалённого сервера БД, по умолчанию: `db`;
- DB_PORT - порт сервера базы данных: `5432`;

Создать и активировать виртуальное пространство, установить зависимости и запустить тесты:

Для Windows:

```python
cd yamdb_final
python -m venv venv
source venv/Scripts/activate
cd api_yamdb
pip install -r requirements.txt
cd ..
pytest
```

Для Mac/Linux:

```python
cd yamdb_final
python3 -m venv venv
source venv/bin/activate
cd api_yamdb
pip install -r requirements.txt
cd ..
pytest
```

Запустить контейнер Docker:

- Проверить статус Docker:

```python
docker --version
```

- Запустить docker-compose:

```python
cd infra/
docker-compose up -d
```

Выполнить миграции, создать суперпользователя и мигрировать статику:

```python
docker-compose exec web python manage.py migrate
docker-compose exec web python manage.py createsuperuser
docker-compose exec web python manage.py collectstatic --no-input
```

Для запуска в виртуальном окружении, после создания и активации виртуального пространства, установки зависимостей, запустить проект локально:

Для Windows:

```python
python manage.py runserver
```

Для Mac/Linux:

```python
python3 manage.py runserver
```

Проверить доступность сервиса:

```python
http://localhost/admin
http://51.250.80.244/admin
```
