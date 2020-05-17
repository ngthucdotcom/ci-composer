# Server Requirements
* OS: Linux 18.04 (recommended)
* PHP: PHP 5.6 or newer

# Installation
## Create project
1. Run composer create project (for init new project) or update (for reload dependencies on new environment) via command line at root folder
* Create project
```shell
composer create-project ngthuc/ci-with-composer
```
* Reload dependencies
```shell
composer update
```
2. Create .env file same [.]env to set-up database
## Require project into another project
1. Run composer require project (for init new project) or update (for reload dependencies on new environment) via command line at root folder
* Require project
```shell
composer require ngthuc/ci-with-composer
```
* Reload dependencies
```shell
composer update
```
2. Move all files from `/vendor/ngthuc/ci-with-composer/app/` to the root folder structure:
```shell
root                          # → Root Directory
└── vendor/
    └── ngthuc/
        └── ci-with-composer/
            └── app/
                ├── apllication/
                ├── public/
                ├── .bowerrc
                ├── .editorconfig
                ├── .gitignore
                ├── .htaccess
                ├── [.]env
                ├── bower.json
                ├── index.php
                └── license.txt
```
3. Create .env file same [.]env to set-up database

# Usage
* Use Apache - MySQL/MariaDB - PHP (AMP) stack as a software (e.g., [XAMPP](https://www.apachefriends.org/index.html)/[AMPPS](https://www.ampps.com/)/[WAMP](http://www.wampserver.com/en/))
* Install AMP stack packages on Linux or Windows, and move project to root directory of Apache (e.g., `www/`) and use [built-in web server](https://www.php.net/manual/en/features.commandline.webserver.php) (with PHP 5.4.0 or newer) via command:
```shell
php -S <address>:<port> -t <YOUR_PROJECT_FOLDER/>
# Example use this command on root directory
php -S localhost:8000
```

## Usage RestAPI

CodeIgniter Rest Server is available on package.

Step 1: Add this to your controller (should be before any of your code)

```php
use chriskacerguis\RestServer\RestController;
```

Step 2: Extend your controller

```php
class Example extends RestController
```

Basic GET example

Here is a basic example. This controller, which should be saved as `Api.php`, can be called in two ways:

* `http://domain/api/users/` will return the list of all users
* `http://domain/api/users/id/1` will only return information about the user with id = 1

```php
<?php
defined('BASEPATH') OR exit('No direct script access allowed');

use chriskacerguis\RestServer\RestController;

class Api extends RestController {

    function __construct()
    {
        // Construct the parent class
        parent::__construct();
    }

    public function users_get()
    {
        // Users from a data store e.g. database
        $users = [
            ['id' => 0, 'name' => 'John', 'email' => 'john@example.com'],
            ['id' => 1, 'name' => 'Jim', 'email' => 'jim@example.com'],
        ];

        $id = $this->get( 'id' );

        if ( $id === null )
        {
            // Check if the users data store contains users
            if ( $users )
            {
                // Set the response and exit
                $this->response( $users, 200 );
            }
            else
            {
                // Set the response and exit
                $this->response( [
                    'status' => false,
                    'message' => 'No users were found'
                ], 404 );
            }
        }
        else
        {
            if ( array_key_exists( $id, $users ) )
            {
                $this->response( $users[$id], 200 );
            }
            else
            {
                $this->response( [
                    'status' => false,
                    'message' => 'No such user found'
                ], 404 );
            }
        }
    }
}
```

# Author
* [Nguyen Thuc](https://ngthuc.github.io/)
* Homepage: ngthuc.com
* Packagist: [CodeIgniter custom core](https://packagist.org/packages/ngthuc/ci-with-composer) by ngthuc
* Email: contact[at]ngthuc.com

# Credit
This project using projects or dependencies:
* CodeIgniter by [B.C. Institute of Technology](https://github.com/bcit-ci/CodeIgniter) (originally from EllisLab).
* PHP dotenv by [vlucas](https://github.com/vlucas/phpdotenv).
* CodeIgniter RestServer by [chriskacerguis](https://github.com/chriskacerguis/codeigniter-restserver)

# License
CodeIgniter Core Custom is licensed under [MIT License](LICENSE).
