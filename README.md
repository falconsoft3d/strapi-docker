# Cómo instalar strapi con docker.

```
$ apt-get update && apt-get upgrade -y
$ apt  install docker.io docker-compose -y

$ sudo apt install curl
$ sudo curl -L "https://github.com/docker/compose/releases/download/1.26.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
$ sudo chmod +x /usr/local/bin/docker-compose
$ sudo docker–compose --version
```

```
$ mkdir strapi
$ cd strapi
$ nano docker-compose.yaml
```


```
version: '3'
services:
  strapi:
    image: strapi/strapi
    environment:
      DATABASE_CLIENT: postgres
      DATABASE_NAME: strapi
      DATABASE_HOST: postgres
      DATABASE_PORT: 5432
      DATABASE_USERNAME: strapi
      DATABASE_PASSWORD: strapi
    volumes:
      - ./app:/srv/app
    ports:
      - '1337:1337'
    depends_on:
      - postgres

  postgres:
    image: postgres
    environment:
      POSTGRES_DB: strapi
      POSTGRES_USER: strapi
      POSTGRES_PASSWORD: strapi
    volumes:
      - ./data:/var/lib/postgresql/data

  pgadmin:
    container_name: pgadmin_container
    image: dpage/pgadmin4
    environment:
      PGADMIN_DEFAULT_EMAIL: 'pgadmin4@pgadmin.org'
      PGADMIN_DEFAULT_PASSWORD: 'pass'

    ports:
      - '5050:80'
    depends_on:
      - postgres      
 ```
 
 
 ```
 $ docker-compose up -d
 ```
 
 
 
