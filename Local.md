
# How to run local dev

# Backend

First of all, you need to run Mysql/MariaDB database, where the application can store its data.
Other prerequisites is to have installed [PHP](https://www.php.net) >= 7.2.5, [composer](https://getcomposer.org/download/) and [Symfony CLI](https://symfony.com/download).
I recommend setting all available on console.

When these criteria are met, you can clone backend project from GitHub.

`git clone https://github.com/privrja/thesis.git`

`cd thesis`

Then you can install dependencies through composer.

`composer install`

To set up connection to your database open file .env and set variable `DATABASE_URL=mysql://user:password@address:port/database_name?serverVersion=X.X`
On the dev server, you should have `APP_ENV=dev` and `APP_DEBUG=1`.

In file Constants.php you should set up ENDPOINT constant, on localhost typically https://localhost:8000/rest/ which is already set.

Then you can fill the database using a script or use a prepared command in composer.json.
To prepare the database and its structure you can run `composer prepare:database:create` this command on the first drop database.
So if you don't have it, it fails. 
This command is better to use in process of development.
When you would like to create database and load data you should use `prepare:database` or `prepare:database:prod`.
So for first, you have to run `php bin/console doctrine:database:create` to create database and `php bin/console doctrine:mig:mig -n` to create tables.

To insert data you can use `php bin/console doctrine:fixtures:load --group=dev -n` --group=dev can be change to prod.
On dev is testing data and in prod, there are more data similar to production.
Same dev/prod difference like in lines above.

But for really production data you need to use [create-insert script]().
For the first run, you need to comment first lines where are commands to drop tables, that you don't have in the database.
But when you used it periodically it can be appropriate to have them there.
Create script assume that database is already created and launched.

To test HTTPS you need to run `symfony server:ca:install`

To start dev server use Symfony CLI `symfony server:start`

To stop server use `symfony server:stop`

To run tests you should run `composer test`

# Frontend

Prerequisites for the frontend is to have [npm](https://www.npmjs.com/get-npm) installed.

Clone project from GitHub.

`git clone https://github.com/privrja/thesis-frontend-react.git`

`cd thesis-frontend-react`

Then install dependecias via npm.

`npm install`

In file Constatns.ts you have to set up backend `ENDPOINT` and `URL_PREFIX` for the frontend. Optionally you can set up several decimal places for mass and set if ID is showing on tables. In Finder, you can set up a **proxy** in ENDPOINTS. Actually is proxy set in files NorineFinder and ChebiFinder on variable `ENDPOINT_URI`.

Run server by
`npm start`

If you would like to build code, run `npm build` and for tests run `npm test`
