Php app

To run the app clone repositories:

```
git clone git@github.com:182Marco/videoBlog-laravel-backend.git
git clone git@github.com:182Marco/videoBlog-nuxt-frontend.git
git clone git@github.com:Gaikanomer9/infra-laravel-nuxt-docker-compose.git
```

Install `Docker` and `Docker-compose` plugin:
```
curl -fsSL https://get.docker.com -o get-docker.sh
sh get-docker.sh
```

After that go to directory `infra-laravel-nuxt-docker-compose` and start the docker compose:

```
cd infra-laravel-nuxt-docker-compose
move .env-example .env
# fill .env with your variables
docker compose up -d
```

To run migrations, find the container with php app running:

```
docker ps
```

Output should like something like that:

```
CONTAINER ID   IMAGE                                   COMMAND                  CREATED       STATUS              PORTS                  NAMES
3666fdc438f7   nginx                                   "/docker-entrypoint.…"   6 days ago    Up About a minute   0.0.0.0:8000->80/tcp   videoblog-nginx
724079a93cc4   infra-laravel-nuxt-docker-compose-app   "docker-php-entrypoi…"   6 days ago    Up About a minute   9000/tcp               videoblog-app
1e1a19d6402a   mysql                                   "docker-entrypoint.s…"   6 days ago    Up About a minute   3306/tcp, 33060/tcp    videoblog-db
```

Notice the ide of the container with `infra-laravel-nuxt-docker-compose-app` image. In this example it's `724079a93cc4`
After that attach to shell on this container and execute commands for migrations:

```
docker exec -it 724079a93cc4 bash
composer install
php artisan migrate
php artisan db:seed
```
