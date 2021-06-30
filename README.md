Container List
-------------------------------

1. PHP
2. Laravel
3. Postgres
4. Artisan
5. NPM
6. Composer

Run and Build Docker Container
-------------------------------

$ docker-compose up -d --build

Bring Down Containers
-------------------------------

$ docker-compose down

Run Single Command (Artisan)
-------------------------------

$ docker-compose run --rm artisan ...	

Run Single Command (NPM)
-------------------------------

$ docker-compose run --rm npm run ...	

Run Single Command (Composer)
-------------------------------

$ docker-compose run --rm composer require ...

