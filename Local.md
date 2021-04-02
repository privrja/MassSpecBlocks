
# How to run local dev

# Backend

First of all you need running Mysql/MariaDB database, where application can store its data.
Other prerequizities is to have installed [PHP](https://www.php.net) >= 7.2.5, [composer](https://getcomposer.org/download/) and [symfony cli](https://symfony.com/download).
I recommend set all available on console.

When this criteria is met you can clone backend project from GitHub.

`git clone https://github.com/privrja/thesis.git`
`cd thesis`

Then you can install dependencies throught composer.

`composer install`

To set up connection to your database open file .env and set variable `DATABASE_URL=mysql://user:password@address:port/database_name?serverVersion=X.X`
On dev server you should have `APP_ENV=dev` and `APP_DEBUG=1`.

In file Constants.php you should set up ENDPOINT constant, on localhost typically https://localhost:8000/rest/ which is already set.

Then you can fill database using script or use prepared command in composer.json.
To prepare database and its structure you can run `composer prepare:database:create` this command on first drop database.
So if you don't have it, it fails. 
This command is better to use in process of development.
When you would like to create database and load data you should use `prepare:database` or `prepare:database:prod`.
So for first, you have to run `php bin/console doctrine:database:create` to create database and `php bin/console doctrine:mig:mig -n` to create tables.

To insert data you can use `php bin/console doctrine:fixtures:load --group=dev -n` --group=dev can be change to prod.
On dev is testing data and in prod, there are more data similar to production.
Same dev/prod difference like in lines above.

But for really production data you need to use [create-insert script]().
For first run, you need to comment first lines where is droping table, that you momentaly don't have in database.
But when you used it periodicaly it can be appropriate to have tham there.
Create script asume that database is already created and launched.

To test https you need to run `symfony server:ca:install`

To start dev server use symfony cli `symfony server:start`

To stop server use `symfony server:stop`

To run test you should run `composer test`

# Frontend

Prerequizities for frontend is to have [npm](https://www.npmjs.com/get-npm) installed.

Clone project fron GitHub.

`git clone https://github.com/privrja/thesis-frontend-react.git`
`cd thesis-frontend-react`

Then install dependecias via npm.

`npm install`

In file Constatns.ts you have to set up backend `ENDPOINT` and `URL_PREFIX` for the frontend. Optionally you can set up a number of decimal places for mass and set if ID is showing on tables. In Finder, you can set up a **proxy** in ENDPOINTS. Actually is proxy set in files NorineFinder and ChebiFinder on variable `ENDPOINT_URI`.

Run server by
`npm start`

If you would like to build code, run `npm build` and for tests run `npm test`
