## Подключаемся по ssh

```
ssh root@ip...

В случае ошибки:

ssh-keygen -R ip...

```

## Обновляем все зависимости, пакеты
```
sudo apt update
```
---

## Удаляет из системы старые версии установленных или обновляемых пакетов, которые больше не нужны

```
sudo apt upgrade
```

## Устанавливаем PHP

> Сам php с драйверами

```
sudo apt install php-fpm php-mbstring php-xml php-bcmath php-curl php-mysql
```
## Установка mysql

```
sudo apt install mysql-server

Заходим в mysql:
sudo mysql

Создаем бд:
CREATE DATABASE laravel_db;

Создаем юзера:
CREATE USER 'dkyshka'@'%' IDENTIFIED WITH mysql_native_password BY 'agdepassword';

Даем полные права на эту бд, но на создания другой бд и т.д. у него прав нет, только у root юзера:
GRANT ALL ON laravel_db.* TO 'dkyshka'@'%';

Выходим:
exit

Заходим под этим юзером:
mysql -u dkyshka -p
agdepassword

Проверяем отображения базы:
SHOW DATABASES;

```

## Установка NGINX сервера

```
sudo apt install nginx
```
## Далее заходим в /etc/nginx/sites-available
> тут будет находится конфигурационный файл для Nginx

--- 
### Устанавливаем консольный редактор Nano если его нет, для редактирования файлов.
> создаем конфигурационный файл например "laravel-api"
---
### Вставляем конфиг
> https://laravel.com/docs/10.x/deployment

Меняем server_name на домен либо ip
Меняем root путь до директории проекта лежащего в /var/www/laravel-api.com/public

```
server_name laravel-api.com www.laravel-api.com
root /var/www/laravel-api/public
```

---

### Далее создаём симлинк (символическая ссылка), с папки sites-available (сайты доступны) до sites-enable (сайты включены)

```
sudo ln -s /etc/nginx/site-available/laravel-api.com /etc/nginx/sites-enabled/
```

---

### Установка Composer

```
sudo apt install composer
```

---

### Далее устанавливаем laravel в директорию /var/www/laravel-api.com/ либо клонируем репозиторий с git

```
composer create-project laravel/laravel .
```
---

### Первоначальная настройка Laravel проекта
> Копируем .env.example в .env

```
cp .env.example .env
```
> Устанавливаем зависимости:
```
composer install --ignore-platform-reqs --no-dev
```
> Генерируем ключ Laravel:
```
php artisan key:generate
```
> Генерируем jwt ключ:
```
php artisan jwt:secret
```
> Даём права на запись в директории кэша, storage:
```
sudo chown -R www-data.www-data /var/www/laravel-api/storage
sudo chown -R www-data.www-data /var/www/laravel-api/bootstrap/cache
```

---
### Установка Git

```
Проверяем на наличие:
git --version 

sudo apt install git
git --version

```

> Указываем глобально user.name / user.email
```
git config --global user.name "имя"
git config --global user.email test@gmail.com

```

---

### Создаём SSH ключ для взаимодействие с приватным репозиторием
```
ssh-keygen -t rsa

cat /root/.ssh/id_rsa.pub

```
> Добавляем ключ в репозиторий

> Проверяем подключение

```
ssh -i /root/.ssh/id_rsa git@github.com

```
> git clone git@github.com:Dkyshka/Laravel_api_backend.git


### Перезагружаем Nginx

```
sudo nginx -t
sudo service nginx restart

```
### Размещение нескольких сайтов
> Прописываем конфиг для нового проекта в /etc/nginx/sites-available/ с новым портом, либо другим доменом

```
server {
    listen 90;
    server_name 91.222.236.123;

    root /var/www/travellist-front;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }

    error_page 404 /error404.html;
}
```
> Прокидываем симлинк, размещаем проект в /var/www/new-project
