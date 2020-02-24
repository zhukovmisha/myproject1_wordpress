# Wordpress

## Setup

I assume you have Ubuntu 18.04

Install Docker

[link](https://docs.docker.com/install/linux/docker-ce/ubuntu/)

Install Docker Compose

[link](https://docs.docker.com/compose/install/)

Create a folder

```
cd ~
mkdir workingdir && cd workingdir && mkdir wordpress && cd wordpress
```

Create a docker-compose.yml file
```
touch docker-compose.yml
```

Open the file using vim

```
vi docker-compose.yml
```

Insert this code there
```
version: '2'
services:
  mariadb:
    image: 'bitnami/mariadb:10.3'
    volumes:
      - 'mariadb_data:/bitnami'
    environment:
      - MARIADB_USER=bn_wordpress
      - MARIADB_DATABASE=bitnami_wordpress
      - MARIADB_PASSWORD=bitnami_password
      - MARIADB_ROOT_PASSWORD=root_password
      - ALLOW_EMPTY_PASSWORD=no
  wordpress:
    image: 'bitnami/wordpress:5'
    ports:
      - '80:80'
      - '443:443'
    volumes:
      - 'wordpress_data:/bitnami'
    depends_on:
      - mariadb
    environment:
      - WORDPRESS_USERNAME=bitnami_user
      - WORDPRESS_PASSWORD=bitnami_wp_password
      - WORDPRESS_DATABASE_USER=bn_wordpress
      - WORDPRESS_DATABASE_NAME=bitnami_wordpress
      - WORDPRESS_DATABASE_PASSWORD=bitnami_password
      - ALLOW_EMPTY_PASSWORD=no
volumes:
  mariadb_data:
    driver: local
  wordpress_data:
    driver: local
```

For further details on Bitnami Images visit [link](https://hub.docker.com/r/bitnami/wordpress)

To spin up wordress
```
docker-compose up -d
```