version: "3"

services:
  flarum:
    image: mondedie/flarum:latest
    container_name: flarum_core
    environment:
      - DEBUG=false
      - FORUM_URL=https://forum.address.com
      - DB_HOST=mariadb
      - DB_NAME=flarum
      - DB_USER=flarum
      - DB_PASS=password
      - DB_PREF=flarum_
      - DB_PORT=3306
      - FLARUM_ADMIN_USER=admin
      - FLARUM_ADMIN_PASS=admin
      - FLARUM_ADMIN_MAIL=email@noted.lol
      - FLARUM_TITLE=Noted Flarum Forum
    volumes:
      - /docker/flarum/assets:/flarum/app/public/assets
      - /docker/flarum/extensions:/flarum/app/extensions
      - /docker/flarum/storage/logs:/flarum/app/storage/logs
      - /docker/flarum/nginx:/etc/nginx/flarum
    ports:
      - 80:8888
    depends_on:
      - mariadb

  mariadb:
    image: mariadb:10.5
    container_name: flarum_mariadb
    environment:
      - MYSQL_ROOT_PASSWORD=changethispassword
      - MYSQL_DATABASE=flarum
      - MYSQL_USER=flarum
      - MYSQL_PASSWORD=changethispassword
    volumes:
      - /docker/flarum/mysql:/var/lib/mysql
