version: '2'

services:
   db:
     image: mysql:5.7
     volumes:
       - db_data:/var/lib/mysql
     restart: always
     environment:
       MYSQL_ROOT_PASSWORD: somewordpress
       MYSQL_DATABASE: wordpress
       MYSQL_USER: wordpress
       MYSQL_PASSWORD: wordpress
     container_name: wp_test_db

   wordpress:
     depends_on:
       - db
     image: wordpress:latest
     ports:
       - "8080:80"
     restart: always
     environment:
       WORDPRESS_DB_HOST: db:3306
       WORDPRESS_DB_USER: wordpress
       WORDPRESS_DB_PASSWORD: wordpress
     container_name: wp_test
     volumes:
    - uploads.ini:/usr/local/etc/php/conf.d/uploads.ini
    
volumes:
    db_data:
