# Trabalhando com Filtros

Os filtros do AngularJS são usados para processar dados e formatar
valores a serem apresentados ao usuário.

A sintaxe geral para usar filtros consiste em usar a sintaxe do Unix
para efetuar um piping do resultado de uma expressão para outra, ou
seja:

```
{{expression | filter}}
```

Ao formatar os dados em tempo de execução, ou seja, utilizar filtros, o
valor desses dados não são alterados, embora o usuário veja o resultado
final formatado.

Pode-se também encadear vários filtros efetuando o piping de um filtro
em outro: A sintaxe é: 

```
{{expression | filter1 | filter2}}
```

Por exemplo:

```
{{ctrl.nome | uppercase | limitTo:4 }}
```

Caso o valor da variável ctrl.nome seja 'Lucas', o output será: `LUCA`.

#### Filtros comuns do AngularJS

- currency
- number 
- lowercase 
- uppercase 
- json
- date
- limitTo
- orderBy
- filter

#### Utilizando filtros em controladores e serviços

Conseguimos utilizar filtros em controladores e serviços desde que os
filtros tenham o sufixo `filter`. No HTML, usa-se a sintaxe de pipe para
fornecer a entrada com a qual os filtros irão trabalhar, seguido de
argumentos opcionais. Quando tivermos de utilizar filtros em
controladores ou serviços, teremos funções.

//TODO exemplo

#### Dica

Se estivermos utilizando filtro diretamente no HTML, eles serão reavaliados
sempre que um ciclo digeste ocorrer. Desse modo, à medida que aumentar a
quantidade de registros que estivermos trabalhando, deveremos estar
cientes do processamento extra que poderá ser realizado quando os
filtros estiverem sendo intensivamente utilizados em nossa UI. Então, se
estivermos trabalhando com arrays grandes e complexos e com estruturas
de dados, deve-se considerar usar os filtros diretamente no controlador
ou serviço. Isso resultará em uma UI mais rápida e responsiva e é
recomendável em relação a aplicar os riltros diretamente em arrays
grandes.
