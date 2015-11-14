# Roteamento em uma Single-Page Aplication

Inicialmente, quando falamos de roteamento em uma Single-Page
Aplication, não estamos falando de URLs-padrão, mas do que é chamado de
URLs hashband. Por exemplo, um URL tradicional poderá se parecer com
`http://www.minhaaplicacaolegal.com/first/page`. Em uma Single-Page
Aplication, esse URL normalmente se aparecerá com `http://www.minhaaplicacaolegal.com.br/#/first/page`. Isso ocorre porque quando o navegador vê uma URL padrão, ele faz uma solicitação ao servidor para acessar o HTML e o JavaScript relevantes para esse URL em particular. Em uma Single-Page Aplication o objetivo é evitar isso e impedir que a página toda seja carregada. Deve-se carregar somente os dados relevantes e partes do HTML em que de acessar todo ele repetidamente, ou seja, qualquer fragmento de URL após o sinal de *#* será ignorado pelo navegador na chamada ao servidor. Quando o navegador se deparar com `http://www.minhaaplicacaolegal.com.br/#/first/page`, ele fará uma solicita;cão ao servidor para `http://www.minhaaplicacaolegal.com.br/`. E quando o usuário navegar de `http://www.minhaaplicacaolegal.com.br/#/first/page` para `http://www.minhaaplicacaolegal.com.br/#/second/page`, o navegador não fará nenhuma solicitação adicional.
