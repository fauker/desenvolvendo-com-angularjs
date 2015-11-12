#Tudo sobre serviços no AngularJS

Quando é dito "serviços" em AngularJS, inclui-se factories, serviços e provedores.

Serviços são Singletons, ou seja, possuem uma única instância no
sistema.

#### O prefixo $ no AngularJS

Serve para identificar os serviços disponibilizados pelo AngularJS.
Quando criarmos nossos próprios serviços, não devemos utilizar o sinal
de $ como prefixo, pois isso pode criar uma confusão para a equipe
posteriormete.

#### Em quais casos devemos criar serviços no AngularJS?

Deve-se criar um serviço no AngularJS se o que estiver sendo
implementado se enquadrar em um dos critérios gerais a seguir:

- (O código deve ser reutilizável)
- (Estados são pertinentes ao nível da aplicação, ou seja, devem ser
  Singletons)
- (É independente da visão)
- (O código se integra com serviços de terceiros)
- (Caching/Factories)

#### A diferença entre factory, serviço e provedor

Deve-se utilizar factory para definir serviços se você:

- (segue um estilo funcional de programação)
- (prefere retornar funções e objetos)

Deve-se utilizar service para definir serviços se você:

- (segue um estilo de programação Classe/OO)

Deve-se utilizar provedores para definir serviços se você:

- (precisa definir alguma configuração para o serviço antes da aplicação
  ser carregada)

Exemplos:

##### Factory:

```
angular.module('app').factory('ItemService', ItemService);

function ItemService() {
  var items = [
    {id: 1, label: 'Item 0'},
    {id: 2, label: 'Item 1'}
  ];

  return {
    list: function() {
        return items;
     },
    add: function(item) {
      items.push(item);
     }
  };
}
```

##### Service

```
angular.module('app').service('ItemService', ItemService);

function ItemService() {
  var items = [
    {id: 1, label: 'Item 0'},
    {id: 2, label: 'Item 1'}
  ];

  this.list = function() {
    return items;
  };

  this.add = function(item) {
    items.push(item);
  };
};
```

**Obs: As duas formas anteriores funcionarão exatamente da mesma
forma.**

##### Provider

O exemplo é um pouco grande, depois eu o coloco aqui. 

