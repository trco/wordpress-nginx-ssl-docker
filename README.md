# wordpress-nginx-ssl-docker

SSL enabled Wordpress website with Nginx and Docker. Inspired by [SSD Nodes blog post](https://blog.ssdnodes.com/blog/host-multiple-ssl-websites-docker-nginx/).

## Prerequisites

1. A server running Linux (tested with Ubuntu 18.04)
2. Docker and Docker Compose installed on your server
3. A registered domain name
4. A DNS A records set up for your server

## Setup

1. SSH into your server, create new folder and clone the repository into it:

```
$ mkdir example && cd example
$ git clone https://github.com/trco/wordpress-nginx-ssl-docker.git .
```

2. Create .env file in root folder and add following variables:

```
MYSQL_ROOT_PASSWORD=example_root_password
MYSQL_DATABASE=example_database
MYSQL_USER=example_user
MYSQL_PASSWORD=example_password
VIRTUAL_HOST=example.com
LETSENCRYPT_HOST=example.com
LETSENCRYPT_EMAIL=example@gmail.com
```

3. Run `docker network create nginx-proxy` to create a unique network for nginx-proxy and other Docker containers to communicate through.

4. Run `docker-compose up -d` inside of nginx-proxy folder. Three containers should initialize:

```
Starting nginx-proxy ... done
Starting nginx-proxy-gen ... done
Starting nginx-proxy-letsencrypt ... done
```

5. Check that containers are up and running with `docker-compose ps`. Debug with `docker-compose logs <container_name>`.

6. Run `docker-compose up -d` inside of the root directory. Two containers should initialize:

```
Starting db ... done
Starting app ... done
```

7. Check that containers are up and running with `docker-compose ps`. Debug with `docker-compose logs <container_name>`.

8. Visit your domain and proceed with Wordpress installation.

## Notes

- You can run multiple dockerized Wordpress websites on single server. Just follow the setup for each website separately.
- You can rename all the containers inside of both docker-compose.yml files.