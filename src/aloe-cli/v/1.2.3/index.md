# Sunset Aloe (BETA)

Aloe CLI v1.1 beta é a segunda versão do Aloe CLI que introduz suporte total para Leaf MVC, novos recursos, melhor suporte para bibliotecas personalizadas e muito mais. O Sunset Aloe também introduz integrações com o Leaf Auth, criando uma opção de scaffolding para tornar a autenticação disponível em seu aplicativo com apenas um comando.

## Novidades

### Melhor suporte para Leaf MVC

O Sunset Aloe é a primeira versão do Aloe integrada com o Leaf MVC. Como tal, ele traz uma integração estreita com o Leaf MVC e as integrações já disponíveis que vêm com o Leaf API. Agora, seu Leaf MVC CLI é alimentado pelo Aloe.

### Autenticação com scaffolding

O Sunset também inclui scaffolding de autenticação que permite adicionar autenticação básica baseada em sessão (login, cadastro, atualização de perfil e guardas) ao seu aplicativo com apenas um comando.

```sh
php leaf scaffold:auth
```

### Atualização de modelos

Estes são modelos básicos gerados quando você executa comandos como g:controller. Estes modelos foram atualizados para mantê-lo atualizado com as atualizações internas e externas do Leaf API e do Leaf MVC.


### Classe de instalação do Aloe

Outra atualização importante do Aloe é a inclusão da Classe de Instalação do Aloe, que basicamente retira o estresse de fazer bibliotecas que precisam instalar arquivos/rotas no diretório de trabalho.

```php
use Aloe\Installer;

Installer::magicCopy($folderToInstall);
Installer::installRoutes("$folderToInstall/routefiles/");
```

**O instalador atualmente só suporta o Leaf MVC e o Leaf API.**

### Pacotes atualizados

Todas as dependências do Aloe foram atualizadas. Isso inclui correções de segurança e uma série de atualizações para manter o Aloe atualizado. Além disso, a biblioteca central por trás do Aloe, o Symfony Console, também foi atualizada, no entanto, fazemos o nosso melhor para manter a sintaxe, a estrutura e a configuração do Aloe CLI, então apesar de todas as atualizações e mudanças externas, o Aloe que você conhece nunca muda.

### Métodos de comando protegidos

Para corresponder ao Symfony Console, o Aloe também usa métodos de comando protegidos nesta versão.

```php
protected function config()
{
    $this
        ->setArgument("argument", "optional", "argument description")
        ->setOption("option", "o", "required", "option description");
}

protected function handle()
{
    $this->comment(
        "example command's output {$this->argument('argument')} {$this->option('option')}"
    );
}
```

## Lista de Comandos do Aloe

```sh
Leaf MVC v2.0

Uso:
  command [opções] [argumentos]

Opções:
  -h, --help            Exibe ajuda para o comando dado. Quando nenhum comando é dado, exibe ajuda para o comando de lista
  -q, --quiet           Não exibe mensagem alguma
  -V, --version         Exibe a versão desta aplicação
      --ansi            Força a saída ANSI
      --no-ansi         Desabilita a saída ANSI
  -n, --no-interaction  Não faz nenhuma pergunta interativa
  -v|vv|vvv, --verbose  Aumenta a verbosidade das mensagens: 1 para saída normal, 2 para saída mais detalhada e 3 para modo de depuração

Comandos disponíveis:
  example        descrição do comando exemplo
  help           Exibe ajuda para um comando
  interact       Interage com a sua aplicação
  list           Lista comandos
  serve          Inicia o servidor de desenvolvimento do Leaf
 aloe
  aloe:config    Instala a configuração do Aloe
 app
  app:down       Coloca a aplicação no modo de manutenção
  app:up         Remove a aplicação do modo de manutenção
 d
  d:command      Apaga um comando de console
  d:controller   Apaga um controller
  d:factory      Apaga uma factory de modelo
  d:migration    Apaga uma migração
  d:model        Apaga um modelo
  d:seed         Apaga um seeder de modelo
 db
  db:install     Cria um novo banco de dados a partir das variáveis .env
  db:migrate     Executa as migrações do banco de dados
  db:rollback    Desfaz todas as migrações do banco de dados
  db:seed        Alimenta o banco de dados com registros
 env
  env:generate   Gera um arquivo .env
 g
  g:command      Cria um novo comando de console
  g:controller   Cria uma nova classe de controller
  g:factory      Cria uma nova factory de modelo
  g:helper       Cria uma nova classe helper
  g:migration    Cria um novo arquivo de migração
  g:model        Cria uma nova classe de modelo
  g:seed         Cria um novo arquivo de seeder
  g:template     Cria um novo arquivo de view
 scaffold
  scaffold:auth  Cria um esqueleto de autenticação básica para a aplicação

```
