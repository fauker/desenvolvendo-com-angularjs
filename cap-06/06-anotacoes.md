# Comunicações com servidores usando $http

#### Melhores práticas

Não utilize o $http direto dos controladores. Encapsule-os em serviços,
da seguinte forma:

```
angular.module('app').factory('UserService', UserService);

UserService.$inject = ['$http'];

function UserService($http) {
  return {
    query: function() {
      return $http.get('/api/users/');
  };
};
```

#### Métodos do $http

- GET
- HEAD
- POST
- DELETE
- PUT
- JSONP


