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
Предоставляет несколько полезных сценариев для добавления и удаления PPA (Personal Package Archive)
sudo apt install software-properties-common

Добавлаем репозиторий пакетов
sudo add-apt-repository ppa:ondrej/php

Обновлаяем пакеты
sudo apt update

Сам php с драйверами
sudo apt install php8.2 php8.2-xml php8.2-curl php8.2-gd php8.2-imagick php8.2-cli  php8.2-mbstring

```
## Установка mysql

```
sudo apt mysql-server
```

## Установка NGINX сервера

```
sudo apt install nginx
```
## Далее заходим в /etc/nginx/sites-available
> тут будет находится конфигурационный файл для Nginx

--- 
### Устанавливаем консольный редактор Nano для редактирования файлов.
> создаем конфигурационный файл например "laravel-api.com"
---
### Вставляем конфиг
> https://laravel.com/docs/10.x/deployment

Меняем server_name на домен
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

### Далее устанавливаем laravel в директорию /var/www/laravel-api.com/

```
composer create-project laravel/laravel .
```
---

### Далее создаём симлинк (символическая ссылка), с папки sites-available (сайты доступны) до sites-enable (сайты включены)

```
sudo ln -s /etc/nginx/site-available/laravel-api.com /etc/nginx/sites-enabled/
```

### Перезагружаем Nginx

```
nginx -s reload
```
