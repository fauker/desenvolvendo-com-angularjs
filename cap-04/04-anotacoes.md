#Formulários, dados de entrada e serviços

##Trabalhando com formulários

Em um formulário comum é recomendado o uso da diretiva ng-submit, na tag
form, ao invés de usar a diretiva ng-click em um botão. Motivos:
utilizando ng-submit um evento de submissão de formulário pode ser
disparado das seguintes formas: clicando no botão Submit ou teclando
Enter em um campo de texto. Já a diretiva ng-click só é acionada quando
o usuário clicar no botão.

//colocar exemplos da forma recomendada e da forma não recomendada.

Ficar atento sempre que for realizar os binds de um formulário. Na
diretiva ng-model, ao invés de passar atributos separadamente, passar
atributos de um objeto, mesmo que ele não tenha sido criado no
controller. Por exemplo:

Ao invés de fazer: 

```
<form ng-submit="submeter()">
  <input type="text" ng-model="ctrl.nome">
  <input type="text" ng-model="ctrl.sobrenome"> 
</form>
``` 

```
Faça:

<form ng-submit="submeter()">
  <input type="text" ng-model="usuario.ctrl.nome">
  <input type="text" ng-model="usuario.ctrl.sobrenome"> 
</form> 
```

No momento em que o usuário digitar algo em um dos campos,
automaticamente o AngularJS criará o objeto **usuario**, na
controller.

##Validação de formulários e estados

Estado do Formulário | Descrição
-------------------- | -------------------------------------
$invalid | Definido quando qualquer campo do formulário estiver inválido
$valid | É o inverso do estado anterior
$pristine | Todos os formulários em AngularJS começam com esse estado. Isso permite descorbrir se um usuário começou a digitar algo e modificou algum dos elementos do formulário.
$dirty | O inverso do $pristine e indica que o usuário fez alguma alteração (elas podem ser desfeitas, porém o $dirty fica ligado).
$error | Armazena todos os campos individuais e os erros em cada elemento do formulário.

// Em leitura.
