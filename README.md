Installation
------------

Launch dockerized environment :

	docker-compose up -d

Log in application docker image :

	docker-compose exec application bash

Install dependencies :

	composer install

Create database if necessary :

  php bin/console doctrine:database:create

Create schemas (FOSUserBundle) :

	php bin/console doctrine:schema:create

Create and activate user :

	php bin/console doctrine:fixtures:load

Access the front end using port 4200 :

	firefox http://localhost:4200 &

Launching tests
---------------

If you want to contribute to project you'll need to have tests to pass. So in order to run them you'll need to :

Log in application docker image :

	docker-compose exec application bash

Update database connection information in `.env.test`

Create database :

  php bin/console doctrine:database:create --env=test

Create schemas (FOSUserBundle) :

	php bin/console doctrine:schema:create --env=test

Create and activate user :

	php bin/console doctrine:fixtures:load --env=test

Copy Phpunit config :

  cp phpunit.xml.dist phpunit.xml

Launch tests using :

  bin/phpunit

Authentication system
---------------------

The Authentication system is based on the JWT token as implemented by [Lexik](https://github.com/lexik/LexikJWTAuthenticationBundle)

User management is done through [FOSUserBundle](https://github.com/FriendsOfSymfony/FOSUserBundle), you can easily add / edit / delete users by using their API.

The server provides a Rest API using [FOSRestBundle](https://github.com/FriendsOfSymfony/FOSRestBundle) allowing you to connect using the following query: 

`curl -X POST -H "Content-Type: application/json" http://localhost:8000/api/login_check -d '{"username":"bob","password":"Abc123"}'`

Client Side specifics
---------------------

On the client side, I've inspired my code from Angular official documentation about HttpInterceptor, allowing me to send the JWT Token on each HTTP request when token is available.

The token is sent in *Authorization* headers: 

`Authorization: Bearer xxx`