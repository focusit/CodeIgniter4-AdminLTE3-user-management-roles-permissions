
CodeIgniter 4 Application Boilerplate
=====================================
![Package](https://img.shields.io/badge/Package-agungsugiarto%2Fboilerplate-light.svg)
[![StyleCI](https://github.styleci.io/repos/243432201/shield?branch=master)](https://github.styleci.io/repos/243432201)
![PHP Composer](https://github.com/agungsugiarto/boilerplate/workflows/PHP%20Composer/badge.svg)
![GitHub All Releases](https://img.shields.io/github/downloads/agungsugiarto/boilerplate/total)
[![GitHub stars](https://img.shields.io/github/stars/agungsugiarto/boilerplate)](https://github.com/agungsugiarto/boilerplate/stargazers)
[![GitHub license](https://img.shields.io/github/license/agungsugiarto/boilerplate)](https://github.com/agungsugiarto/boilerplate/blob/master/LICENSE.md)

Feature
-------
* Configurable backend theme [AdminLTE 3](https://adminlte.io/docs/3.0/)
* Css framework [Bootstrap 4](https://getbootstrap.com/)
* Icons by [Font Awesome 5](https://fontawesome.com/)
* Role-based permissions provided by [Myth/Auth](https://github.com/lonnieezell/myth-auth)
* Menu dynamically
* Localized English / Indonesian

This project is early on development feel free to contribute
------------------------------------------------------------
Screenshoot | Demo On [Heroku](https://boilerplate-codeigniter4.herokuapp.com/)
-------------------------------------------------------------------------------
![Dashboard](.github/dashboard.png?raw=true)

Installation
------------
first of all Install the latest version of compososer becasue composer 1.10 has been depricated.

**1.** Get The Module
Before you install via composer you must install fresh ci4-framework 
 require via composer

```bash
composer create-project codeigniter4/appstarter your-project-name
```
After that you must set the composer.json minimum stability add with code bellow
```
"minimum-stability": "dev",
```
 
 add the module
 
 require via composer

```bash
composer require agungsugiarto/boilerplate
```

**2.** Set CI_ENVIRONMENT, base url, index page, and database config in your `.env` file based on your existing database (If you don't have a `.env` file, you can copy first from `env` file: `cp env .env` first). If the database not exists, create database first.

```bash
# .env file
CI_ENVIRONMENT = development

app.baseURL = 'http://localhost:8080'
app.indexPage = ''

database.default.hostname = localhost
database.default.database = boilerplate
database.default.username = root
database.default.password =
database.default.DBDriver = MySQLi
```
**3.** Run publish auth
```bash
php spark auth:publsih

Publish Migration? [y, n]: n
Publish Models? [y, n]: n
Publish Entities? [y, n]: n
Publish Controller? [y, n]: n
Publish Views? [y, n]: n
Publish Config file? [y, n]: y
  created: Config/Auth.php
Publish Language file? [y, n]:
```

> NOTE: Everything about how to configure auth you find add [Myth/Auth](https://github.com/lonnieezell/myth-auth).


Its done ? not to fast. After the publish `Config/Auth.php` you need to change
`public $views` with below like this.
```php
public $views = [
    'login'           => 'agungsugiarto\boilerplate\Views\Authentication\login',
    'register'        => 'agungsugiarto\boilerplate\Views\Authentication\register',
    'forgot'          => 'agungsugiarto\boilerplate\Views\Authentication\forgot',
    'reset'           => 'agungsugiarto\boilerplate\Views\Authentication\reset',
    'emailForgot'     => 'agungsugiarto\boilerplate\Views\Authentication\emails\fogot',
    'emailActivation' => 'agungsugiarto\boilerplate\Views\Authentication\emails\acivation',
];
```

Open `app\Config\Filters.php` see at `$aliases` add with below like this.
```php
public $aliases = [
	#after the default code
	'login'      => \Myth\Auth\Filters\LoginFilter::class,
	'role'       => \agungsugiarto\boilerplate\Filters\RoleFilter::class,
	'permission' => \agungsugiarto\boilerplate\Filters\PermissionFilter::class,
];
```

**4.** Run publish, migrate and seed boilerplate
```bash
php spark migrate -all
```
(While migration if you encounter error sqlite3 class not found install php-sqlite using ofllowing command

```bash
sudo apt install php-sqlite3
```



```bash
php spark boilerplate:install
```

**5.** Run development server:

```bash
php spark serve
```

**6.** Open in browser http://localhost:8080/admin
```bash
Default user and password
+----+--------+-------------+
| No | User   | Password    |
+----+--------+-------------+
| 1  | admin  | super-admin |
| 2  | user   | super-user  |
+----+--------+-------------+
```

Settings
--------

Config Boilerplate

You can configure default dashboard controller and backend theme in `app\Config\Boilerplate.php`,

```php
class Boilerplate extends BaseConfig
{
    public $appName = 'Boilerplate';

    public $dashboard = [
        'namespace'  => 'agungsugiarto\boilerplate\Controllers',
        'controller' => 'DashboardController::index',
        'filter'     => 'permission:back-office',
    ];
// App/Config/Boilerplate.php
```

Usage
-----
You can find how its work with the read code routes, controller and views etc. Finnaly happy coding!

Contributing
------------
Contributions are very welcome.

License
-------

This package is free software distributed under the terms of the [MIT license](LICENSE.md).
