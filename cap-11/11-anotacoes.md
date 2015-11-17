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

#### A função link

A função link faz pela diretiva o que um controlador faz uma visão -
define APIs e funções necessárias à diretiva, além de manipular e
trabalhar com o DOM.

O AngularJS executa a função link para cada instância da diretiva,
portanto cada instância pode ter sua própria lógica de negócios completa
e contida, sem afetar nenhuma outra instância da diretiva. A função
*link* recebe um conjunto-padrão de argumentos, que permanece
consistente entre as diretivas e é semelhante a:

```
link: function($scope, $element, $attrs) {}
```

Obs: tomar cuidado para não utilizar o $scope de forma indevida, pois
ele pode afetar o $scope do controlador, por default.

#### Escopo

Por padrão, toda diretiva herda o escopo de seu pai, que é passado a ela
na função *link*.

O AngularJS disponibiliza a chave *scope* n objeto de definição da
diretiva para termos controle completo sobre o escopo do elemento
relacionado à diretiva. A palavra *scope* pode assumir três valores:

- **false**: É o valor default. Diz que o escopo da diretiva é
  exatamente igual ao escopo do pai. Portanto a diretiva terá acesso a
todas as variáveis e funções definidas no escopo-pai, e qualquer
modificação feita se refletirá imediatamente no pai também.

- **true**: Diz ao AngularJS que o escopo da diretiva herda o
  escopo-pai, porém um escopo-filho próprio será criado. A diretiva
então terá acesso a todas as variáveis e funções do escopo-pai, porém
qualquer modificação que ela fizer não estartá disponível no pai.

- **object**: Também podemos passar um objeto com chaves e valores para
  o escopo. Isso diz ao AngularJS para criar um **escopo isolado**. Esse
escopo não herda nada do pai e qualquer dado que o escopo-pai deva
compartilhar com essa diretia deverá ser passado por meio de atributos
HTML. É a melhor opção quando estivermos criando componentes
reutilizáveis que devam ser independentes de como e onde eles serão
usados.

Para o objeto podemos especificar três tipos d evalores que podem ser
passados, e que o AngularJS colocará diretamente no escopo da diretiva.
São eles:

- *=*: O sinal de *=* especifica que o valor do atributo no HTML deverá
  ser tratado como um objeto JSON, que será associado ao escopo da
diretiva de modo que qualquer alteração feita no escopo-pai estará
automaticamente disponível na diretiva.

- *@*: O sinal de *@* especifica que o valor do atributo no HTML deverá
  ser tratado como uma string, que poderá ou não ter expressões de
binding do AngularJS `({{}})`. O valor deverá ser calculado e o valor
final será atribuído ao escopo da diretiva. Qualquer alteração no vaor
também estará disponível na diretiva.

- *&*: O sinal de *&* especifica que o valor do atributo no HTML é uma
  função de algum controlador cuja referência deverá estar disponível à
diretiva. A diretiva pode então disparar a função sempre que for
necessário.

#### replace

Está obsoleto.


