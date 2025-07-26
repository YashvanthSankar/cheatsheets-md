# AngularJS

## Basics

- **AngularJS**: JavaScript MVC framework, version 1.x (not Angular 2+)
- **Key Concepts**: Modules, Controllers, Directives, Services, Data Binding, Dependency Injection

---

## Setup

```html
<!-- Include AngularJS from CDN -->
<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.8.2/angular.min.js"></script>

<!-- App Declaration -->
<html ng-app="myApp">
</html>
```

---

## Module

```js
var app = angular.module('myApp', []);
```

---

## Controller

```js
app.controller('MainCtrl', function($scope) {
  $scope.greeting = "Hello, AngularJS!";
});
```
```html
<div ng-controller="MainCtrl">
  {{ greeting }}
</div>
```

---

## Data Binding

- **Interpolation**: `{{ expression }}`
- **ng-model**: Two-way binding

```html
<input ng-model="name">
<p>Hello {{ name }}</p>
```

---

## Directives

- Built-in: `ng-app`, `ng-model`, `ng-repeat`, `ng-if`, `ng-show`, `ng-hide`, `ng-click`, `ng-submit`, `ng-class`
- Custom Directives:

```js
app.directive('myDirective', function() {
  return {
    template: '<div>Custom Directive!</div>'
  };
});
```

---

## Filters

```html
{{ 1234.5678 | number:2 }}    <!-- 1,234.57 -->
{{ "hello" | uppercase }}     <!-- HELLO -->
{{ "hello" | lowercase }}     <!-- hello -->
{{ dateObj | date:'yyyy-MM-dd' }}
```

Common filters: `currency`, `date`, `json`, `limitTo`, `orderBy`

---

## Services

- Built-in: `$http`, `$timeout`, `$interval`, `$location`, `$window`
- Custom:

```js
app.service('myService', function() {
  this.sayHello = function() { return "Hello!"; };
});
```

Inject service:

```js
app.controller('Ctrl', function($scope, myService) {
  $scope.msg = myService.sayHello();
});
```

---

## Dependency Injection

- Inject dependencies via function parameters.

```js
app.controller('Ctrl', ['$scope', '$http', function($scope, $http) {
  // ...
}]);
```

---

## Routing (ngRoute)

```html
<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.8.2/angular-route.js"></script>
```
```js
app.config(function($routeProvider) {
  $routeProvider
    .when('/home', {
      templateUrl: 'home.html',
      controller: 'HomeCtrl'
    })
    .otherwise({redirectTo: '/home'});
});
```
```html
<div ng-view></div>
```

---

## $http Service (AJAX)

```js
$http.get('/api/items').then(function(response) {
  $scope.items = response.data;
});
```
```js
$http.post('/api/add', {name: 'Item'}).then(function(response) {
  // handle response
});
```

---

## Forms & Validation

```html
<form name="myForm">
  <input ng-model="user.email" required>
  <span ng-show="myForm.email.$error.required">Required!</span>
</form>
```

---

## Events

```html
<button ng-click="doSomething()">Click Me</button>
```
```js
$scope.doSomething = function() { alert('Clicked!'); }
```

---

## ng-repeat

```html
<ul>
  <li ng-repeat="item in items">{{ item.name }}</li>
</ul>
```

---

## Scope Hierarchy

- `$scope`: Each controller has its own scope
- `$rootScope`: Shared across app

---

## Custom Filters

```js
app.filter('reverse', function() {
  return function(input) {
    return input.split('').reverse().join('');
  };
});
```
```html
{{ 'hello' | reverse }} <!-- olleh -->
```

---

## Built-in Services

- `$http`, `$q` (promises), `$timeout`, `$interval`, `$filter`, `$location`, `$window`, `$rootScope`

---

## Promises

```js
$http.get('/api/data').then(function(response) {
  $scope.data = response.data;
}, function(error) {
  // error handling
});
```

---

## Animations (ngAnimate)

```html
<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.8.2/angular-animate.js"></script>
```

---

## Useful CLI Commands (for AngularJS projects)

- No official CLI, but use `bower`, `npm`, or manual file management.

---

## Best Practices

- Use `controllerAs` syntax for clarity
- Minimize use of `$scope` (prefer `this`)
- Organize code by modules
- Prefer one-way data flow where possible

---

## Debugging

- Use browser DevTools
- Use `ng-inspector` browser extension

---

## Migration

- AngularJS is legacy (Angular 2+ is recommended for new projects). Migration tools: [Angular Upgrade Guide](https://angular.io/guide/upgrade)

---

**Tip:** Always separate concerns (controllers for logic, views for UI, services for data/communication).

---

## Reference

- [AngularJS Official Docs](https://docs.angularjs.org/)
- [AngularJS API Reference](https://docs.angularjs.org/api)
