## 1. Construir Imagen
docker build -t ecos/apache Docker

## 2. Levntar mysql
docker run -p 3306:3306 --name ecos-mysql -e MYSQL_ROOT_PASSWORD=superSecret -d mysql

## 3. Levantar aplicación
docker run -d -v /Users/gfarias/Workspace/ecos-docker/ws2-intermedio:/var/www/ -p 80:80 --name ecos-app --link ecos-mysql ecos/apache

## 4. Crear base de datos desde mysql
docker exec ecos-app mysql -uroot -psuperSecret -h ecos-mysql -P 3306 -e "create database ecos;"

## 5. Migrar datos
docker exec ecos-app php artisan migrate --seed
