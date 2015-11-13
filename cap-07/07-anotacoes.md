# Testes de Unidade em Serviços e em XHRs

#### Testes de unidade em chamadas ao servidor

Para realizar testes de unidade em chamadas ao servidor, deve-se
utilizar um serviço chamado **$httpBackend**. O serviço **$http** usa
**$httpBackend** internamente para fazer solicitações XHR propriamente
ditas. Lembrando que, para utilizar o **$httpBackend**, é necessário ter
o arquivo *angular-mocks.js*.
