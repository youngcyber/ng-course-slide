## Chapter 07 - Dependency Injection

---

### File Structure

	chapter07.html
	app/
		07/
			app.js

---

### Example Usage

	app.controller('HomeController', function($scope, $http, xxx) {
	});

---

### Value

app.js

	var app = angular.module('app', []);

	app.value('accessToken', 'xxx');

	app.value('currentUser', {
		name: 'admin'
	});

	app.value('helloValue', function() {
		return 'Hello, Value';
	});

---

### Value (2)

app.js

	app.controller('HomeController',
		function(accessToken, currentUser, helloValue) {

		console.log(accessToken);
		accessToken = 'yyy';
		console.log(accessToken);

		currentUser.name = 'kongthap';
		console.log(currentUser.name);

		console.log(helloValue());
	});

---

### Constant

app.js

	app.constant('apiUrl', '//api-slim.tutor4dev.com');

	app.constant('config', {
		xxx: 'x',
		yyy: 'y'
	});

---

## Quiz 07-1

---

### Service

app.js

	app.service('helloService', function() {
		this.hello = function() {
			return 'Hello, Service';
		}
	});

	app.controller('HomeController', function(helloService) {
		console.log(helloService.hello());
	});

---

### Factory

app.js

	app.factory('helloFactory', function() {
		return {
			hello: function() {
				return 'Hello, Factory';
			}
		};
	});

	app.controller('HomeController', function(helloFactory) {
		console.log(helloFactory.hello());
	});

---

### Service VS Factory

	app.service('helloService', function() {
		this.hello = function() {
			return 'Hello, Service';
		}
	});

	app.factory('helloFactory', function() {
		return {
			hello: function() {
				return 'Hello, Factory';
			}
		};
	});

---

## Quiz 07-2

---

### Provider

app.js

	app.provider('hello', function() {
		var text = 'xxx';

		return {
			setText: function(value) {
				text = value;
			},
			$get: function() {
				return {
					hello: function() {
						return 'Hello, Provider: ' + text
					}
				}
			}
		}
	});

---

### Provider (2)

app.js

	app.controller('HomeController', function(helloProvider) {
		console.log(helloProvider.hello());
	});

	app.config(function(helloProvider) {
		helloProvider.setText('yyy');
	});

---

## Quiz 07-3

---

## Quiz 07-4

---

### Chapter 07 - End
