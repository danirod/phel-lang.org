+++
title = "Getting started"
weight = 1
+++

## Requirements

Phel requires PHP 8.0 or higher and [Composer](https://getcomposer.org/).

## Quick start

To get started right away, you can use the [cli-skeleton project on GitHub](https://github.com/phel-lang/cli-skeleton).

```bash
git clone https://github.com/phel-lang/cli-skeleton.git
composer install
# Start the REPL to try Phel
./vendor/bin/phel repl
```

More information can be found in the Readme of the project.

## Manually initialize a new project using Composer

The easiest way to get started is by setting up a new Composer project. First, create a new directory and initialize a new Composer project.

```bash
mkdir hello-world
cd hello-world
composer init
```

Composer will ask a bunch of questions that can be answered as in the following example.

```
Welcome to the Composer config generator

This command will guide you through creating your composer.json config.

Package name (<vendor>/<name>): phel-lang/hello-world
Description []:
Author [Your Name <your.name@domain.com>, n to skip]:
Minimum Stability []:
Package Type (e.g. library, project, metapackage, composer-plugin) []: project
License []:

Define your dependencies.

Would you like to define your dependencies (require) interactively [yes]? no
Would you like to define your dev dependencies (require-dev) interactively [yes]? no

{
    "name": "phel-lang/hello-world",
    "type": "project",
    "authors": [
        {
            "name": "Your Name",
            "email": "your.name@domain.com"
        }
    ],
    "require": {}
}

Do you confirm generation [yes]? yes
```

Next, require Phel as a dependency.

```bash
# Require and install Phel
composer require phel-lang/phel-lang
```

First, create a phel config file, called `phel-config.php` in the root of the project:

```php
<?php

return (new \Phel\Config\PhelConfig())
    ->setSrcDirs(['src'])
;
```

> Read the docs for [Configuration](/documentation/configuration) to see all available configuration options for Phel.

Then, create a new directory `src` with a file `boot.phel` inside this directory.

```bash
mkdir src
```

The file `boot.phel` contains the actual code of the project. It defines the namespace and prints "Hello, World!".

```phel
# in src/boot.phel
(ns hello-world\boot)

(println "Hello, World!")
```


## Running the code

There are two ways to run the code: from the command line and with a PHP Server.


### From the Command line

Code can be executed from the command line by calling the `vendor/bin/phel run` command, followed by the file path or namespace:

```bash
vendor/bin/phel run src/boot.phel
# or
vendor/bin/phel run hello-world\\boot
# or
vendor/bin/phel run "hello-world\boot"
```

The output will be:

```
Hello, World!
```


### With a PHP Server

> Check the [web-skeleton project on GitHub](https://github.com/phel-lang/web-skeleton).

The file `index.php` will be executed by the PHP Server. It initializes the Phel Runtime and loads the namespace from the `boot.phel` file described above, to start the application.

```php
// src/index.php
<?php

use Phel\Phel;

$projectRootDir = __DIR__ . '/../';

require $projectRootDir . 'vendor/autoload.php';

Phel::run($projectRootDir, 'hello-world\\boot');
```

The PHP Server can now be started.

```bash
# Start server
php -S localhost:8000 ./src/index.php
```

In the browser, the URL `http://localhost:8000` will now print "Hello, World!".


## Launch the REPL

To try Phel you can run a REPL by executing the `./vendor/bin/phel repl` command.

> Read more about the [REPL](/documentation/repl) in its own chapter.

## Editor support

Phel comes with basic support for <a href="https://github.com/phel-lang/phel-vs-code-extension" target="_blank">
VSCode</a>, <a href="https://github.com/phel-lang/phel-phpstorm-syntax" target="_blank">PhpStorm</a>
and a <a href="https://codeberg.org/mmontone/interactive-lang-tools/src/branch/master/backends/phel" target="_blank">
Emacs mode with interactive capabilities</a> in the making.
