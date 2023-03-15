# Aloe CLI

O Aloe é um serviço de console simples, porém poderoso, que torna a construção de seus aplicativos Leaf uma tarefa fácil. O Aloe CLI vem com a ferramenta padrão de console Leaf nas novas versões do Leaf API, Leaf MVC e Skeleton.

O Aloe vem com um conjunto predefinido de comandos que fornecem criação de projetos, gerenciamento de banco de dados e aplicativos diretamente do console. Ele também introduz uma maneira muito mais simples e limpa de escrever seus comandos.

## Lista de Comandos do Aloe

```bash
ALOE

Uso:
  command [options] [arguments]

Opções:
  -h, --help            Exibe esta mensagem de ajuda
  -q, --quiet           Não exibe nenhuma mensagem
  -V, --version         Exibe a versão desta aplicação
      --ansi            Força a saída ANSI
      --no-ansi         Desabilita a saída ANSI
  -n, --no-interaction  Não faz nenhuma pergunta interativa
  -v|vv|vvv, --verbose  Aumenta a verbosidade das mensagens: 1 para saída normal, 2 para saída mais verbosa e 3 para saída de depuração

Comandos disponíveis:
  example        Descrição do comando exemplo
  help           Exibe ajuda para um comando
  interact       Interage com seu aplicativo
  list           Lista de comandos
  serve          Inicia o servidor de desenvolvimento do Leaf
 aloe
  aloe:config    Instala a configuração do Aloe
 app
  app:down       Coloca o aplicativo no modo de manutenção
  app:up         Remove o aplicativo do modo de manutenção
 d
  d:command      Exclui um comando do console
  d:controller   Exclui um controlador
  d:factory      Exclui uma fábrica de modelos
  d:migration    Exclui uma migração
  d:model        Exclui um modelo
  d:seed         Exclui uma semeadora de modelos
 db
  db:install     Cria um novo banco de dados a partir das variáveis .env
  db:migrate     Executa as migrações do banco de dados
  db:rollback    Reverte todas as migrações do banco de dados
  db:seed        Popula o banco de dados com registros
 env
  env:generate   Gera um arquivo .env
 g
  g:command      Cria um novo comando do console
  g:controller   Cria uma nova classe de controlador
  g:factory      Cria uma nova fábrica de modelos
  g:helper       Cria uma nova classe auxiliar
  g:migration    Cria um novo arquivo de migração
  g:model        Cria uma nova classe de modelo
  g:seed         Cria um novo arquivo de semeadora
  g:template     Cria um novo arquivo de visualização
 scaffold
  scaffold:auth  Cria uma autenticação básica do aplicativo

```
