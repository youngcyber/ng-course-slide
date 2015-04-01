### Chapter 03 - AngularJS Application

#### File Structure

	chapter03.html
	app/
		03/
			app.js

---

### AngularJS Application

app.js

	var app = angular.module('app', []);

chapter03.html

	<!DOCTYPE html>
	<html ng-app="app">
	<head>
		<title>AngularJS - Course</title>
	</head>

	<body>

		<script src="angular.min.js"></ script>
		<script src="app/03/app.js"></ script>

	</ body>
	</ html>

---

### Controller

app.js

	app.controller('BasicController', function() {

		console.log('Hello, World');

	});

chapter03.html

	<div ng-controller="BasicController">
	</div>

---

### `$scope`

app.js

	app.controller('BasicController', function($scope) {

		$scope.name = 'AngularJS';

		$scope.hello = function() {
			console.log('Hello, ' + $scope.name);
		}

	});

chapter03.html

	<div ng-controller="BasicController">

		{{ name }}
		<br>
		<button ng-click="hello()">Hello</button>

	</div>

---

## Quiz 03-1

---

### `ng-repeat`

app.js

	app.controller('EmployeeController', function($scope) {
		$scope.employees = [
			{
				"emp_no":"10001",
				"birth_date":"1953-09-02",
				"first_name":"Georgi",
				"last_name":"Facello",
				"gender":"M",
				"hire_date":"1986-06-26"
			}
		]
	});

chapter03.html

	<div ng-controller="EmployeeController">

		<p ng-repeat="e in employees">{{ e }}</p>

	</div>

---

## Quiz 03-2

---

### `ng-repeat` with Filter

All fields

	<input type="text" ng-model="query" placeholder="Search">
	<p>{{ query }}</p>

	<p ng-repeat="e in employees | filter: query">
		{{ e }}
	</p>

Specified field

	<input type="text" placeholder="Last Name"
		ng-model="query.last_name">

---

### `ng-repeat` with Sort

Ascending

	<input type="radio" ng-model="sort" value="first_name">

	<input type="radio" ng-model="sort" value="last_name">

Descending

	<input type="radio" ng-model="sort" value="-first_name">

`ng-repeat`

	<p ng-repeat="e in employees | orderBy: sort">
		{{ e }}
	</p>

---

## Chapter 03 - End
