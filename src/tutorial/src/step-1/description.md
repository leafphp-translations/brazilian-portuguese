# Como começar

Bem vindo ao tutorial do framework Leaf!

Esta é uma tentativa de lhe mostrar como trabalhar com Leaf framework. 
O objetivo é lhe dar os conhecimentos necessários para construir um 
aplicativo simples, você não precisa entender tudo para continuar, 
no entanto, depois de conclui-lo, é aconselhável ler a documentação que detalham cada tópico.

## PRÉ REQUISITOS

O tutorial presume que você tem conhecimento básico de PHP. 
Se não tiveres experiência com PHP, pode não ser uma boa ideia pular 
a introdução ao framework e os primeiros passos - [entender o básico](https://www.w3schools.com/php/default.asp)
e então voltar! Experiência com outros frameworks pode ajudar, mas não é um requisito.

## COMO USAR ESSE TUTORIAL

Você pode editar o código <span class="wide">a direita</span><span class="narrow">below</span> e ver o resultado quando clicar no botão "RUN" que se encontra a direita após o bloco "preview". 

<details>
<summary>Opções de execução</summary>

Como Leaf framework permite que você crie multiplas rotas, adicionamos um arquivo `request.json` no editor que é responsável pela execução do código.
O arquivo se parece com o abaixo, por padrão:
```json
{
  "method": "GET",
  "path": "/",
  "data": {}
}
```

You can tell the editor to run a post, put, patch, delete or options request instead of a GET request by updating the `method`. You can change the route to run by updating the `path` and even pass in `data` which the editor should run your code with. This can be GET or POST request data.
</details>

<details>
<summary>Passos do tutorial</summary>


Each step will introduce a core feature of Leaf, and you will be expected to complete the code to get the demo working. If you get stuck, you will have a "Show me!" button that reveals the working code for you. Try not to rely on it too much - you'll learn faster by figuring things out on your own.

If you are an experienced developer coming from Leaf 2 or other frameworks, there are a few settings you can tweak to make the best use of this tutorial. If you are a beginner, it's recommended to go with the defaults.
</details>

<details>
<summary>Detalhes do tutorial</summary>

- Leaf framework oferecer dois estilos de API: funcional e orientado a objetos. This tutorial is designed to work for both - you can choose your preferred style using the **Style preference** switches at the top. <a target="_blank" href="/docs/introduction/#class-mode-vs-functional-mode">Learn more about API styles</a>.

</details>

Pronto para iniciar a sua jornada? Clique em "Próximo" para iniciar.
