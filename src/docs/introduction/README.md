# Introduction

::: tip NOTE
Already know Leaf 2 and just want to learn about what's new in Leaf 3? Check out the [Migration Guide](/docs/migration/introduction.html)!
:::

## What is Leaf PHP?

Leaf is a PHP framework that helps you create clean, simple but powerful web apps and APIs quickly and easily. Leaf introduces a cleaner and much simpler structure to the PHP language while maintaining it's flexibility. With a simple structure and a shallow learning curve, it's an excellent way to rapidly build powerful and high performant web apps and APIs.

The core library is focused on the REST APIs only, and is easy to pick up and integrate with other libraries or existing projects. On the other hand, Leaf is also perfectly capable of powering sophisticated MVC Applications with it's wide library of modules.

<!-- If you’d like to learn more about Leaf before diving in, we created a video walking through the core principles and a sample project.

<VideoLesson href="https://youtube.com/" title="Watch a free video course on Leaf Mastery">Watch the leaf 3 intro video on youtube</VideoLesson> -->

## Getting Started

::: tip Quick Tip
The official guide assumes basic level knowledge of PHP. If you are totally new to PHP, you might want to take an introduction course - grasp the basics then come back! This is because you will basically be writing PHP code when using leaf (or any other framework).
:::

### [Installation instructions here](/docs/introduction/installation.html)

Below is a hello world example which takes you through the core of Leaf. You can check out [more advanced examples](/examples/) for more useful examples. If you want to build a real world app, you can refer to our [codelab experiments](/codelabs/) for real world examples and use-cases.

## Hello world example

At the core of Leaf PHP is a system that enables us to declaratively define applications using a friendly and straightfoward syntax:

**index.php:**

```php
<?php

require __DIR__ . "/vendor/autoload.php";

$app = new Leaf\App;

$app->get("/", function () {
  echo "Hello world";
});

$app->run();
```

We have already created our very first Leaf app! This is as simple as it gets.

In addition, we can output data with `Leaf\Http\Response`. This is a module which allows us to output data of various types without any hussle.

```php
<?php

require __DIR__ . "/vendor/autoload.php";

use Leaf\Http\Response;

$app = new Leaf\App;

$app->get("/", function () {
  Response::markup("Hello world");
});

$app->run();
```

Now you might be wondering why we need ro go through all of this just to return some html when we can just use echo. The reason for this is simple. `Response` takes care of a whole lof issues for us under the hood and renders exactly what we expect. Let's look at an example below.

```php
<?php

require __DIR__ . "/vendor/autoload.php";

$app = new Leaf\App;

$app->get("/", function () {
  // set content-type to json
  Leaf\Http\Headers::contentJSON();

  echo "<b>Hello world</b>";
});

$app->run();
```

When we run this, we get:

```json
"<b>Hello world</b>"
```

instead of

```html
Hello World
```

Unlike the confusion above between the content type and echo, response makes sure that whatever content we're trying to render reflects in the content type. This is just one of the many things that response takes care of automatically.

### Handling User Input

One very important part of building web apps/APIs is user input. Users may pass data into your leaf app through forms, http request bodies, urls, ...

You must read this data and make sure it can't harm your system before performing any operations on it. This can be very clumsy when done raw with PHP, especially when the data comes in through multiple channels. Leaf has however prepared a simple handler for this: `Leaf\Http\Request`.

<!-- user goes to /?greeting=hello%20world -->

```php
<?php

require __DIR__ . "/vendor/autoload.php";

use Leaf\Http\Request;
use Leaf\Http\Response;

$app = new Leaf\App;

$app->get("/", function () {
  // we can get the GET request data from the URL like this
  $greeting = Request::get("greeting"); // hello world

  // output json encoded data
  Response::json([
    "greeting" => $greeting
  ]);
});

$app->run();
```

The most beautiful thing about the request object is that all data passed into your app is automatically sanitized to prevent attacks like XSS. You have simple and safe code working for you.

### Installing modules

Modules are pieces of functionality that have been packaged and shipped separately from Leaf core. Modules are used to extend Leaf's reach to perform some operations not available on the core. Modules were introduced with Leaf 3, but some of them can be used with earlier versions of Leaf. Modules can also be used in external libraries and frameworks as well. To install a module, simply run it's install script with composer.

To demonstrate this, we will expand the app above to output a template instead of the json data from earlier. For this, we will need a template module. Leaf has 3 template modules

- BareUI: Super lightweight, blazing fast templating engine with zero compilation
- Blade: A port of the laravel blade templating engine
- Leaf Veins: Lightweight but powerful templating

For this demo, we will use bareUI. We can install bareUI with composer.

```sh
composer require leafs/bareui
```

After this, leaf automatically links the bareUI class for you and makes it available on the leaf object as `template`. So from there, we can do create our template. I'll name this `index.view.php` (bare ui templates end in `.view.php`)

```php
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  <h2><?php echo $greeting; ?></h2>
</body>
</html>
```

The next thing to do is to tell bareUI where to look for templates and finally render `index.view.php`.

```php
<?php

require __DIR__ . "/vendor/autoload.php";

use Leaf\Http\Request;
use Leaf\Http\Response;

$app = new Leaf\App;

// point to the templates directory
$app->template->config("path", "./");

$app->get("/", function () use($app) {
  // we can get the GET request data from the URL like this
  $greeting = Request::get("greeting"); // hello world

  // render our template
  $app->template->render("index", [
    "greeting" => "Hello universe",
  ]);
});

$app->run();
```

Just as you saw above, most Leaf modules require absolutely no configuration in order to work with leaf core. They just fit right in.

## "Functional Mode"

We have mostly talked about general features which are the same even in Leaf 2, now let's talk about some spice in Leaf 3. This is just an introduction to functional mode, read the [functional mode documentation](/docs/functional-mode.html) for the full explanation.

Basically, leaf 3 comes with global helper functions which take away the only pain anyone has ever had in using leaf, i.e. long namespaces. Let's rewrite the first example in functional mode.

```php
<?php

require __DIR__ . "/vendor/autoload.php";

app()->get("/", function () {
  // we can get the GET request data from the URL like this
  $greeting = request("greeting");

  // output json encoded data
  json(["greeting" => $greeting]);
});

app()->run();
```

You notice that we've gotten rid of the lengthy namespaces and even the leaf initializer. Leaf 3 helps you focus on only what matters: your application. Everything is either done for you under the hood or the provided to you in simple to use tools.

## Ready for More?

We've briefly introduced the most basic features of Leaf 3 - the rest of this guide will cover them and other advanced features with much finer details, so make sure to read through it all!