<div id="header" align="center">
  <img src="https://media.giphy.com/media/du3J3cXyzhj75IOgvA/giphy.gif" width="600"/>
</div>

```

Устанавливаем laravel c базой PostgreSQL и кэшем Redis

curl -s "https://laravel.build/laravel-api?with=pgsql,redis" | bash

---

Далее в docker-compose.yml файле дополняем конфигурацию - установив контейнер adminer, для управления БД

depends_on:
	- adminer


И сам образ по порту 8080:

adminer:
    image: adminer
    restart: always
    networks:
        - sail
    ports:
        - '8080:8080'
    depends_on:
        - pgsql



Доступы лежат в конфигурационном файле .env


---
---
Далее можем создавать Контроллеры и Модели и фиксировать Контроллеры в route

sail artisan make:controller Api/V1/UserController --model=User (Если модель существует, то доп. атрибут проигнорируется)

```