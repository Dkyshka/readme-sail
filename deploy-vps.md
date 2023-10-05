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

```

Сам php с драйверами
sudo apt install php-fpm php-mbstring php-xml php-bcmath php-curl php-mysql
```
## Установка mysql

```
sudo apt install mysql-server

Создаем бд
CREATE DATABASE laravel_db;

Создаем юзера
CREATE USER 'dkyshka'@'%' IDENTIFIED WITH mysql_native_password BY 'agdepassword';

Даем полные права на эту бд, но на создания другой бд и т.д. у него прав нет, только у root юзера
GRANT ALL ON laravel_db.* TO 'dkyshka'@'%';

Выходим
exit

Заходим под этим юзером
mysql -u dkyshka -p
agdepassword

Проверяем отображения базы
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
> создаем конфигурационный файл например "laravel-api.com"
---
### Вставляем конфиг
> https://laravel.com/docs/10.x/deployment

Меняем server_name на домен либо ip
Меняем root путь до директории проекта лежащего в /var/www/laravel-api.com/public

```
server_name laravel-api.com www.laravel-api.com
root /var/www/laravel-api.com/public
```
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

### Установка Git

```
git --version

sudo apt install git

git --version
```

### Далее создаём симлинк (символическая ссылка), с папки sites-available (сайты доступны) до sites-enable (сайты включены)

```
sudo ln -s /etc/nginx/site-available/laravel-api.com /etc/nginx/sites-enabled/
```

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
