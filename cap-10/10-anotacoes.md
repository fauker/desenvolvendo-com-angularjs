# Roteamento em uma Single-Page Aplication

Inicialmente, quando falamos de roteamento em uma Single-Page
Aplication, não estamos falando de URLs-padrão, mas do que é chamado de
URLs hashband. Por exemplo, um URL tradicional poderá se parecer com
`http://www.minhaaplicacaolegal.com/first/page`. Em uma Single-Page
Aplication, esse URL normalmente se aparecerá com `http://www.minhaaplicacaolegal.com.br/#/first/page`. Isso ocorre porque quando o navegador vê uma URL padrão, ele faz uma solicitação ao servidor para acessar o HTML e o JavaScript relevantes para esse URL em particular. Em uma Single-Page Aplication o objetivo é evitar isso e impedir que a página toda seja carregada. Deve-se carregar somente os dados relevantes e partes do HTML em que de acessar todo ele repetidamente, ou seja, qualquer fragmento de URL após o sinal de *#* será ignorado pelo navegador na chamada ao servidor. Quando o navegador se deparar com `http://www.minhaaplicacaolegal.com.br/#/first/page`, ele fará uma solicita;cão ao servidor para `http://www.minhaaplicacaolegal.com.br/`. E quando o usuário navegar de `http://www.minhaaplicacaolegal.com.br/#/first/page` para `http://www.minhaaplicacaolegal.com.br/#/second/page`, o navegador não fará nenhuma solicitação adicional.

#### Usando ngRoute.  Passos.

1. Incluir o arquivo **angular-route.js** depois de **angular.js** ter
   sido carregado para tornar o módulo `ngRoute` disponível.

2. No HTML, deve-se marcar em que ponto queremos que o roteamento tenha
   efeito usando a diretiva `ng-view`.

3. Quando o módulo da aplicação for criado, deve-se especificar que ele
   depende do módulo `ngRoute` (usando `angular.module('app',
['ngRoute'])`).

4. Por fim, deve-se definir as rotas na seção `config` do *AngularJS*
   usando `$routeProvider`.

O `$routeProvider` permite definir as rotas em um só local por meio da
função `when()`. Essa função aceita dois argumentos:

- O primeiro é uma URL ou uma regex de URL que especifica quando essa
  rota em particular é aplicável.

-  O segundo é um objeto de configuração que especifica o que deve
   acontecer quando a rota em particular é encontrada.

Exemplo:

```
angular.module('app', ['ngRoute']).config('$routeProvider',
function($routeProvider) {
  $routeProvider.when('/', {
    template: '<h5>Essa é a rota padrão</h5>'
  })

  .when('/usuarios/', {
    tempalte: '<h5>Essa é a rota que lista os usuários</j5>'
  })
}
```

#### Opções de roteamento

A sintaxe da função `when()` completa é a seguinte:

```
$routeProvider.when(url, {
  template: string,
  templateUrl: string,
  controller: string, function or array,
  controllerAsL: string,
  resolve, object<key, function>
});
```

Obs: no objeto do `$routeProvider`, podemos definir um alias para o
controlador de duas formas: 

`controller: MyCtrl as Ctrl`

ou 

```
controller: MyCtrl,
controllerAs: Ctrl
```

***Ambas dão na mesma! A escolha é questão de gosto pessoal.***

Obs: Quando declaramos o controller no `$routeProvider`, não precisamos
utilizar a diretiva `ng-controller` em nosso HTML.

#### Usando resolver para veriicações prévias na rota
