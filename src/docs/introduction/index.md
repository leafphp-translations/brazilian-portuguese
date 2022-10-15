<!-- markdownlint-disable no-inline-html -->
# Introdução

::: tip ⚡️ Oficial Release
Está é a documentação do Lead v3.0

- [**Leaf 2 docs**](https://archive.leafphp.dev)
- [**Leaf 1 docs**](https://v1.leafphp.dev)
:::

<script setup>
import VideoDocs from '/@theme/components/VideoDocs.vue'
</script>

## O que é Leaf PHP?

Leaf é um pequeno e leve framework PHP para iniciar aplicativos web e APIs limpos, simples, mas poderosos, de forma rápida e fácil. Ao longo dos anos, nós temos nos concentrado em entregar software mais simples e com mais perfomance, que podem ser usado em todos seus aplicativos PHP.

A versão 3 do Leaf tem mais a oferecer com temática centrada na experiência e a usabilidade do desenvolvedor, mas com todas vantagens garantindo que os usuários também tenham a melhor experiência.

[→ Checkout Leaf 3's features](/docs/introduction/features)

## Iniciando

Este guia presume que você tenha um conhecimento **básico** de PHP.

::: warning 😵‍💫 Não conheço PHP?
Se você não tem conhecimento com PHP, nós recomendamos que você confira o [W3Schools PHP Tutorial](https://www.w3schools.com/php/default.asp) antes de continuar. Quando você usa Leaf (ou outro framework) você está basicamente escrevendo código PHP.
:::

### Instalação

<VideoDocs
  subject="Watch the leaf 3 installation walkthrough"
  description="Throughout the leaf documentation, you will see video links like the one just below. If you are a visual learner, this gives you another way to follow along with our documentation. We call these the video docs."
  link="https://www.youtube.com/embed/PuOk5xqTIsA"
/>

Para iniciar rapidamente com o Leaf, veja nosso [guia de instalção](/docs/introduction/installation.html). Isso lhe dá a você uma explicação detalhada de como montar o projeto com leaf de várias maneiras.  

::: tip Migrando
Já conhece Leaf 2 e quer saber o que há de novo no Leaf 3? Veja o [Guia de migração](/docs/migration/introduction.html)!
:::

Abaixo temos um exemplo de "Olá Mundo" que leva você ao core do Leaf. Outras partes da documentação tem exemplos mais detalhados.
Você também pode consultar nosso [experimentos com codelab](https://codelabs.leafphp.dev) para exemplos do mundo real e estudos de caso.

## Exemplo "Olá Mundo"

No core do Leaf PHP o temos  um sistema que permite
que nós definamos e declaremos aplicações usando uma
sintaxe amigável e direta.

**index.php:**

<div class="class-mode">

```php
<?php

require __DIR__ . '/vendor/autoload.php';

$app = new Leaf\App;

$app->get('/', function () {
  echo 'Olá mundo';
});

$app->run();
```

</div>
<div class="functional-mode">

```php
<?php

require __DIR__ . '/vendor/autoload.php';

app()->get('/', function () {
  echo 'Olá mundo';
});

app()->run();
```

</div>

Nós já criamos nossa primeira aplicação Leaf!
Isto é o mais simples que podemos imaginar.

Além disso, podemos fazer o retorno com Leaf response.
Esse módulo nos permite ter vários tipos de retorno sem esforço.  

<div class="class-mode">

```php
<?php

require __DIR__ . '/vendor/autoload.php';

$app = new Leaf\App;

$app->get('/', function () use($app) {
  $app->response()->markup('Olá mundo');
});

$app->run();
```

Agora você pode estar se perguntando, porque nós precisamos de tudo isso
apenas para retornar HTML quando poderíamos utilizar apenas `echo`. A razão para isso é simples
`Response` resolve muitos problemas "por baixo dos panos" e faz exatamente o que é esperado.
Veja um exemplo abaixo.

</div>
<div class="functional-mode">

```php
<?php

require __DIR__ . '/vendor/autoload.php';

app()->get('/', function () {
  response()->markup('Olá mundo');
});

app()->run();
```

Nós usamos `response` ao invés `echo`
porque isso renderiza examente o que esperamos.
Veja um exemplo abaixo.

</div>

<div class="class-mode">

```php
<?php

require __DIR__ . '/vendor/autoload.php';

$app = new Leaf\App;

$app->get('/', function () {
  // set content-type to json
  Leaf\Http\Headers::contentJSON();

  echo '<b>Hello world</b>';
});

$app->run();
```

</div>
<div class="functional-mode">

```php
<?php

require __DIR__ . '/vendor/autoload.php';

app()->get('/', function () {
  // set content-type to json
  Leaf\Http\Headers::contentJSON();

  echo '<b>Olá mundo</b>';
});

app()->run();
```

</div>

Quando executamos esse emplos, nós obtemos "\<b>Olá mundo\</b>" ao invés de **Olá mundo**

Ao contrário da confusão acima entre o `content type` e `echo`, Leaf response garante
que o conteúdo reflita o `content type`. Esta é apenas uma das muitas coisas que o `response`  se encarrega de fazer
de forma transparente

## Modo Funcional

Nós temos principalmente falado sobre as caracteriscas gerais que são as mesmas que temos no Leaf 2,
então vamos falar sobre o "tempero" adicionado ao Leaf 3

::: tip
Está é apenas uma introdução ao modo funcionado. Leia a [documentçao para o modo funcional](/docs/tooling/functions.html) para uma explicação completa.
:::

Basicamente Leaf 3 vem com um helper global de funções que tiram a única dor
que alguém já teve ao usar o Leaf, ou seja, longos `namespaces` e instanciação de classes.
Vamos reescrever nosso primeiro exemplo de modo funcional

```php
<?php

require __DIR__ . '/vendor/autoload.php';

app()->get('/', function () {
  response()->markup('Olá mundo');
});

app()->run();
```

Você deve notar que nos livramos de `use Leaf\Http\Response;` e também da instanciação da classe do Leaf. O Leaf 3
ajuda a se concentrar no realmente importa: a lógica da sua aplicação. Tudo é feito pelo framework e
dispobilizado através de ferramentas fáceis de usar.

### Trabalhando com entrada de dados

Uma parte muito importe da construção de web apps/APIs é a entrada de dados pelo usuário.
Usuários podem enviar dados para seu aplicativo atráveis de formulários, http request, bodys, URLs, etc...

Você deve ler estes dados e certificar-se que eles não podem quebrar seu sistema antes de realizar qualquer operação.
Isso pode ser muito complicado se utilizarmos PHP puro, especialmente quanto há multiplos pontos de entrada. Leaf, entretanto, tem um manipulador simples para isso: `Leaf\Http\Request`. Como estamos utilizando o modo funcionando, nós vamos usar o método `request` no lugar da classe.

O usuário vai para /?greeting=hello%20world

```php
<?php

require __DIR__ . '/vendor/autoload.php';

app()->get('/', function () {
  // we can get the GET request data from the URL like this
  $greeting = request()->get('greeting'); // hello world

  // output json encoded data
  response()->json([
    'greeting' => $greeting
  ]);
});

app()->run();
```

A beleza sobre o objeto `request` é que todos os dados que passam pelo aplicativo são sanitizados automaticamente e evitam ataques como XSS. Você tem um código mais simples e seguro.

## Orientado a objetos vs modo funcional

Leaf suporta duas maneiras diferentes de você escrever seu código.

- Usando modo funcional que vimos acima.
- Usando o modo orientado a objetos que tem sido usado desde de Lead v1.

### Orientado a objetos

Está é a maneira padrão da maior parte dos frameworks.
Com Leaf foi contruído seguindo orientação,  você pode contruir sua aplicação inteira de modo orientado a objetos. 
Como utilizando a classe `Leaf\Http\Response`.

```php
<?php

require __DIR__ . "/vendor/autoload.php";

$app = new Leaf\App;

$app->get("/", function () {
  echo "Olá mundo";
});

$app->run();
```

### Modo funcional

Classes tornam-se incomodas de usar e repetidas, especialmente por causa dos `namespaces`. Você também pode precisar, algumas vezes, 
colocar a instância de uma classe dentro do escopo de uma função, utilizando `use`. 
Pegar a instância de uma classe pode ser difícil, algumas vezes, o que leva a reinicialização da classe. 
Por essas razões (e outras), nós criamos  funções sem escopo que permite rapidamente construir aplicações. Essas funções devolvem instâncias de classes do framework para que você não precise usar as classes diretamente.

```php
<?php

require __DIR__ . "/vendor/autoload.php";

app()->get("/", function () {
  echo "Hello world";
});

app()->run();
```

## Modes in the docs

Just as leaf allows you to write your code in 2 ways, with functional mode or class mode, our docs come with examples prepared for both.

You can click on this switch in the sidebar to toggle the mode of the examples on our documentation.

![Switcher](https://user-images.githubusercontent.com/26604242/178108346-c9c22a19-6a82-4786-ac3e-00cbfe69cba8.png)

## Installing modules

Modules are pieces of functionality that have been packaged and shipped separately from the Leaf core. Modules are used to extend Leaf's reach by performing operations not available on the core. Modules were introduced with Leaf 3, but some of them can be used with earlier versions of Leaf. Modules can also be used in external libraries and frameworks as well. To install a module, simply run its install script with composer or use the leaf CLI.

To demonstrate this, we will expand the app above to output a template instead of the JSON data from earlier. For this, we will need a template module. Leaf has 3 template modules

- BareUI: Super lightweight, blazing fast templating engine with zero compilation
- Blade: A port of the laravel blade templating engine
- Leaf Veins: Lightweight but powerful templating

For this demo, we will use BareUI. We can install BareUI with leaf CLI.

```sh
leaf install bareui
```

Or with composer:

```sh
composer require leafs/bareui
```

After this, Leaf **automatically** links the BareUI class for you and makes it available on the leaf object as `template`. So from there, we can create our template. I'll name this `index.view.php` (BareUI templates end in `.view.php`)

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

The next thing to do is to tell BareUI where to look for templates and finally render `index.view.php`.

<div class="class-mode">

```php
<?php

require __DIR__ . "/vendor/autoload.php";

$app = new Leaf\App();

// point to the templates directory
$app->template->config("path", "./");

$app->get("/", function () use($app) {
  // we can get the GET request data from the URL like this
  $greeting = $app->request()->get("greeting"); // hello world

  // render our template
  echo $app->template->render("index", [
    "greeting" => $greeting,
  ]);
});

$app->run();
```

</div>
<div class="functional-mode">

```php
<?php

require __DIR__ . "/vendor/autoload.php";

// point to the templates directory
app()->template->config("path", "./");

app()->get("/", function () {
  // we can get the GET request data from the URL like this
  $greeting = request()->get("greeting"); // hello world

  // render our template
  echo app()->template->render("index", [
    "greeting" => $greeting,
  ]);
});

app()->run();
```

</div>

Just as you saw above, most Leaf modules require absolutely no configuration in order to work with the Leaf core. They just fit right in.

## Pronto para mais?

We've briefly introduced the most basic features of Leaf 3 - the rest of this guide will cover them and other advanced features in much finer detail, so make sure to read through it!

## Próximos passos

If you skipped the [Introduction](/guide/introduction), we strongly recommend reading it before moving on to the rest of the documentation.

<div class="vt-box-container next-steps">
  <a class="vt-box" href="/docs/introduction/installation">
    <h3 class="next-steps-link">Continue the Guide</h3>
    <small class="next-steps-caption">The guide walks you through every aspect of the framework in full details.</small>
  </a>
  <a class="vt-box" href="/docs/introduction/first-app">
    <h3 class="next-steps-link">Follow the Tutorial</h3>
    <small class="next-steps-caption">For those who prefer learning things hands-on. Let's build something real!</small>
  </a>
  <a class="vt-box" href="https://codelabs.leafphp.dev" target="_blank">
    <h3 class="next-steps-link">Check out CodeLabs</h3>
    <small class="next-steps-caption">Codelabs provides interactive tutorials with in-depth explanations.</small>
  </a>
</div>
