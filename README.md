# Docker-compose-lamp
> https://github.com/sprintcube/docker-compose-lamp.git



## Запускаем Docker Desktop и dockerd
* sudo dockerd
* в www кладём php - сайт
* в config/initdb кладём базу (.sh, .sql, .sql.gz and .sql.xz)
* docker compose up -d
* docker compose stop
* docker compose start



## Запуск bash в container
`docker exec -it 0724f6d13e2e bash`



## Смена владельца на /var/www/html
TODO надо сделать чтобы docker автоматом это делал
```
docker exec -it CONTAINER_HASH_NAME bash
cd /var/www/html
chown -R www-data:www-data ./favicons ./wp-admin ./wp-includes

cd wp-content/
chown -R www-data:www-data ./plugins ./cache ./languages/ ./settings/ ./upgrade/ ./uploads ./uploads-adaptive

# или убрать временно папку с темой www/wp-content/themes/sitename и:
chown -R www-data:www-data ./
# - и затем вернуть папку с темой (так как в ней мы работаем из основной ОС а не из докера)
```



## При пересборке images если меняется версия mysql (а может и php - надо проверить), надо удалить содержимое и проверить права на data/mysql:
data/mysql



## vhosts 
config/vhosts/default.conf



## Как настраиватеся БД в WP
1. В phpmyadmin (http://localhost:8080/) нужно выставить полные привелегии для user "docker" на БД "sitename.com"
2: www/wp-config.php:
   !!! database:3306 - как отображается в phpmyadmin (http://localhost:8080/) наверху слева
```
define('DB_NAME', 'sitename.com');
define('DB_USER', 'docker');
define('DB_PASSWORD', 'docker');
define('DB_HOST', 'database:3306');
```



## ? Изменение прав на файлы через Dockerfile
RUN usermod -u 1000 www-data



## ? mysql "user: mysql" https://github.com/sprintcube/docker-compose-lamp/issues/221#issuecomment-1368099894
database:
  user: mysql



## ? php "user: www-data" 
webserver:
  user: www-data