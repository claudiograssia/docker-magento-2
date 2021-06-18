# Magento 2 Deploy

Use this guide in order to speed up build last version for magento 2

### Prerequisite
To have installed docker

### Prepare the env 
After clone launch this command inside folder docker-magento-2
```sh
docker-compose --build
```
this command can be take some minutes.

After that launch
```sh
docker-compose start magento_php
```
After start, we need to entry inside container with this command
```sh
docker exec -it mag_php bash
```
inside container we need to download magento
please launch these commands:
note: command composer will ask us the magento credential for download magento 2 library.
```sh
su magento
rm -rf /var/www/html/*
composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition . 
```

After that we ready for install magento
Please close the container terminal and start the other container with this command:
```sh
docker-compose up -d
```
this command will start the other container  for example, nginx, elasticsearch and mysql

Please enter again in the php container:
```sh
docker exec -it mag_php bash
```
and launch this command in order to install magento:
```sh
su magento
php bin/magento setup:install \
--base-url=http://www.test.com \
--db-host=mag_mysql \
--db-name=magento \
--db-user=magento \
--db-password=magento \
--admin-firstname=admin \
--admin-lastname=admin \
--admin-email=admin@admin.com \
--admin-user=admin \
--admin-password=admin123 \
--language=en_US \
--currency=USD \
--timezone=Europe/Rome \
--use-rewrites=1 \
--search-engine=elasticsearch7 \
--elasticsearch-host=mag_elastic \
--elasticsearch-port=9200
```

### Enjoy your environment