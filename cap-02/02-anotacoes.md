## Sintaxe de injeção de dependências e o AngularJS

- Não recomendado:

  ```
  angular.module('app').controller('SomeCtrl', function(dependency) {
    
  });
  ```

- Recomendado pelo livro:

  ```
  angular.module('app').controller('SomeCtrl', ['dependency', function () {
    
  }]);
  ```

- Recomendado pelo John Papa

  ```
  angular.module('app').controller('SomeCtrl', SomeCtrl);

  SomeCtrl.$inject = ['dependency'];

  function SomeCtrl() {
 
   }
  ```

Motivo: o modo não recomendado pode causar problemas ao minificarmos
nosso código.


=======================================

### $scope versus sintaxe controllerAs

- A vantagem do controllerAs em relação ao $scope é que as variáveis ou
as funções disponibilizadas pelo controlador e a instância do
controlador ficam explícitas no HTML. Em uma UI complicada e aninhada,
não será preciso brincar de "Onde está Wally?" para encontrar as
variáveis em seu código. Isso se torna óbvio de imediato porque a
instância do controlador estará presente no HTML.

//TODO exemplos

### this em JavaScript

- Pessoas acostumadas a linguagens como Java têm problemas para
  compreender a palavra-chave this em JavaScript. Uma das
características loucas e insanas (e definitivamente interessantes) do
JavaSript é que a palavra-chave this em uma função pode ser sobrescrita
por quem quer que chame a função. Desse modo, o this dentor e fora de
uma função pode se referir a dois objetos ou escopos totalmente
diferentes. 
Sendo assim, em geral, é melhor atribuir a referência this em um
controlador a uma variável proxy e sempre referenciar a instância por
meio desse proxy (self, por exemplo) para garantir que a instância a que
estamos nos referindo seja a instância correta.

//TODO exemplos

### Usando ng-bind versus chaves duplas
- A vantagem do ng-bind em relação à notação de chaves duplas é que o
  AngularJS consome tempo para inicializar e executar até que ele possa
encontrar e substituir todas as chaves duplas do HTML. Isso significa
que, durante alguns instantes em que o navegador é iniciado, você poderá
ver chaves duplas aparecendo na UI até que o AngularJS tenha a primeira
carga da página, e não em visões carregadas posteriormente. Esse
problema não ocorrerá com ng-bind.


