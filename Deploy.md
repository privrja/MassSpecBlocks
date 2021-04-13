
# How to deploy on server

## Database

Use create/insert script to prepare database structure [create-insert-script.sql](https://github.com/privrja/MassSpecBlocks/blob/main/create-insert-script.sql). Script at start contains drops for tables and constraints. If you don't have these tables in the database before, you should comment first part of the script. The script assumes that the database was already created and launched.

## Backend

### Checkout project
```git clone https://github.com/privrja/thesis.git```

```cd thesis/```

### Setup

In .env file setup connection to the database and other properties.

`APP_ENV=prod`

`APP_DEBUG=0` or remove this line, because when APP_ENV is set up to prod then this is automatically set to zero.

Setup `APP_SECRET` to a random hexadecimal 32 length string.

`DATABASE_URL=mysql://user:password@address:port/databaseName?serverVersion=version`

example for MariaDB: `DATABASE_URL=mysql://***@***.***:3306/msb?serverVersion=mariadb-10.4.17`

Mail configuration is in .env too.

To set up logging you need to set variable `SHELL_VERBOSITY`. Values for this are -1 (Error), 1 (Notice), 2 (Info), 3 (Debug). The log is stored to `var/log/dev.log`.

In file `src/Constant/Constants`.php you should set up `ENDPOINT` and `LOGOUT_TIME` constants.

Use `composer dump-env prod` for creating .env.local.php

### Install dependencies

Install dependencies via Composer. Install it. Composer is available at [https://getcomposer.org/download/](https://getcomposer.org/download/).

After that, you need to install dependencies. 

`composer install --no-dev --optimize-autoloader`

**--no-dev** only when v APP_ENV is **prod**

### Upload

Before upload, you should execute.

`php bin/console cache:clear`

To server, you should upload folders `src, vendor, config, public`.

Var folder is created automatically, it can fail when the application has not permission to create a folder, or you can upload it.

To check if is running, access it on the browser. On /api/doc would be a web page with documentation. Address /rest should return 401, because you need to log in.

After that, you should log in as default users and change passwords to them. (Recommended to do this using frontend)

### Frontend

Clone project from GitHub.

`git clone https://github.com/privrja/thesis-frontend-react.git` 

```cd thesis-frontend-react/```


You need to install dependencies using npm. Tutorial for installing npm is [here](https://www.npmjs.com/get-npm). After that only type: 
`npm install --production`.

In file src/constant/Constants.ts you have to set up backend `ENDPOINT` and `URL_PREFIX` for the frontend. Optionally you can set up several decimal places for mass and set if ID is showing on tables. In Finder, you can set up a proxy in ENDPOINTS. Actually is proxy set in files `src/finder/NorineFinder` and `src/finder/ChebiFinder` on variable `ENDPOINT_URI`.

After that, you can build the frontend using `npm build`. This creates a folder build that you would transfer to the server.
