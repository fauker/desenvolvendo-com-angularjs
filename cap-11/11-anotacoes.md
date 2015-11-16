# Diretivas

As diretivas constituem a maneira de o AngularJS lidar com manipulação
de DOM e renderizar widgets de UI reutilizáveis.

#### Alternativas para diretivas personalizadas

##### ng-include

Se tivermos arquivos HTML extensos, podemos facilmente serpará-los em
arquivos HTML menores e mais fáceis de ser administrados e tornar nosso
HTML modular.

Exemplo:

```
<div ng-include="'views/usuario.html'">
</div>
```

##### ng-switch

*ng-switch* é outra diretiva que nos permite adicionar algumas
funcionalidades à UI para exibir determinados trechos de HTML de forma
seletiva. Ela nos proporciona uma maneira de uncluir trechos de HTML
condicionalmente ao se comportar como um swtich/case diretamente no
HTML. Aqui está um uso simples de *ng-switch*:


```
<html>
<head>
  <title>Aplicação</title>
</head>
<body ng-app="switchApp">

  <div ng-controller="MainCtrl as mainCtrl">
    <h3>Conditional Elements in HTML</h3>
    <button ng-click="mainCtrl.currentTab = 'tab1'">
      Tab 1
    </button>
    <button ng-click="mainCtrl.currentTab = 'tab2'">
      Tab 2
    </button>
    <button ng-click="mainCtrl.currentTab = 'tab3'">
      Tab 3
    </button>
    <button ng-click="mainCtrl.currentTab = 'something'">
      Trigger Default
    </button>

    <div ng-switch="mainCtrl.currentTab">
      <div ng-switch-when="tab1">
        Tab 1 is selected
      </div>
      <div ng-switch-when="tab2">
        Tab 2 is selected
      </div>
      <div ng-switch-when="tab3">
        Tab 3 is selected
      </div>
      <div ng-switch-default>
        No known tab selected
      </div>
    </div>
  </div>

  <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.3.11/angular.js"></script>
  <script type="text/javascript">
    angular.module('switchApp', [])
        .controller('MainCtrl', [function() {
          this.currentTab = 'tab1';
        }]);
  </script>
</body>
</html>
```

#### Criando uma diretiva

Criamos diretivas da mesma forma que criamos controladores, serviços, e
filtros.

```
angular.module('app').directive('nomeDaDiretiva', nomeDaDiretiva);

function nomeDaDiretiva() {
  return {
    // Definição da diretiva
  };
};
```

##### Template/URL de template

O primeiro item que podemos definir como parte de nossa diretiva é
verificar se ela tem algum conteúdo que deva ser inserido quando a
diretiva for encontrada pelo AngularJS. Fazemos isso usando as chaves
*template* e *templateUrl* do objeto de definição da diretiva.
(semelhante ao roteamento).

- template: inserimos o HTML inline;
- templateUrl: inserimos a página HTML.

##### restrict 

A palavra-chave *restrict* define o modo como alguém deve usar a
diretiva em seu código. Quando criamos nossa diretiva, temos o controle
para decidir como ela deve ser usada. Por exemplo:

- A: a diretiva pode ser usada somente como *Atributo*. Ex: `<div
  minha-diretiva>`.

- E: a diretiva pode ser usava somente como *Elemento*. Ex:
  `<minha-diretiva/>`.

- C: a diretiva pode ser usada somente como *Classe*. Ex: `<div class="minha-diretiva"/>`.

- M: a diretiva pode ser usada somente como um *Comentário HTML*. Ex:
  `<!-- directive: minha-diretiva -->`.

Essas opções podem ser usadas separadamente ou podem ser combinadas umas
com as outras. Por exemplo:

`restrict: AE` define que nossa diretiva pode ser utilizada como
*atributo* e *elemento*, e nunca como *classe*. Exemplo:

permitido: `<div minha-diretiva/>` e `<minha-diretiva/>`
não permitido: `<div class="minha-diretiva"/>`

*Dicas*:

- As diretivas baseadas em classe são ideais para tarefas relacionadas à
  renderização. Por exemplo: a diretiva *ng-cloak* que oculta e mostra
elemtnos ou as diretivas para carga de imagens).

- As diretivas de elemtno são recomendadas se estivermos criando um
  conteúdo HTML totalmente novo.

- as diretivas de atributo normalmente são preferíveis para mudanças de
  comportamento. Por exemplo: ng-show, ng-class e assim por diante.
