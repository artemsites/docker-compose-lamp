* Запускаем Docker Desktop
* в www кладём php - сайт
* в config/initdb кладём базу (.sh, .sql, .sql.gz and .sql.xz)
* docker compose up -d
* docker compose stop
* docker compose start



## Смена владельца на /var/www/html
### TODO надо сделать чтобы docker автоматом это делал
docker exec -it CONTAINER_HASH_NAME bash
cd /var/www/html
chown -R www-data:www-data ./



## При пересборке images если меняется версия mysql (а может и php - надо проверить), надо удалить содержимое и проверить права на data/mysql:
data/mysql



# ? "user: mysql" https://github.com/sprintcube/docker-compose-lamp/issues/221#issuecomment-1368099894
database:
  user: mysql



```
/** Имя базы данных для WordPress */
define('DB_NAME', 'yamdiet.com');

/** Имя пользователя MySQL */
define('DB_USER', 'docker');

/** Пароль к базе данных MySQL */
define('DB_PASSWORD', 'docker');

/** Имя сервера MySQL */
define('DB_HOST', 'database:3306');
```