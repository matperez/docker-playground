# Структруа каталогов

В корне должен лежать docker-compose.yml, запускающий все сразу.

В нем должны запускаться базы elasticsearch и mysql, а так же, наверное, nginx и php-fpm, потому что отдельно на каждый сервис запускать эти сервисы нет смысла. Nginx должен различать хосты по номеру порта, а не по имени, так как имя в разных окружениях может различаться.

Дополнительные хосты можно добавить в nginx/default.conf ниже основновного хоста.

## Запуск
```
docker-compose up
```
## Админка MYSQL
После запуска Adminer доступен по адресу http://localhost:8080 

## Установка пакетов и применение миграций
```
docker-compose exec php bash
cd /var/www/app
composer install --prefer-dist -vv
php ./yii init --env=Development-Docker --overwrite=y
php ./yii migrate
```


