## Chapter 05 - Modularized Application

---

### File Structure

	chapter05.html
	app/
		05/
			app.js
			employee.js

---

### Using `ngAnimate`

app.js

	var app = angular.module('app', ['ngAnimate']);

	app.controller('EmployeeController', function($scope, $http) {
		$http.get('http://api-slim.tutor4dev.com/employees.json')
			.success(function(data) {
				$scope.employees = data;
			});
	});

---

### Using `ngAnimate` (2)

chapter05.html `<style>`

	<style>
		.ng-enter {
			transition:0.75s;
			opacity:0;
		}
		.ng-enter-active {
			opacity:1;
		}
		.ng-leave {
			transition:0.75s;
			opacity:1;
		}
		.ng-leave-active {
			opacity:0;
		}
	</style>

---

### Using `ngAnimate` (3)

chapter05.html

	<body>
		<div ng-controller="EmployeeController">
			<input type="text" ng-model="query">
			<p ng-repeat="e in employees | filter: query">
				{{ e.first_name + ' ' + e.last_name }}
			</p>
		</div>

		<script src="angular.min.js"></ script>
		<script src="angular-animate.min.js"></ script>

		<script src="app/05/app.js"></ script>
	</ body>

---

### Modularized AngularJS Application

app.js

	var app = angular.module('app', ['employeeModule']);

employee.js

	var emp = angular.module('employeeModule', []);

	emp.controller('EmployeeController', function($scope, $http) {

		$http.get('http://api-slim.tutor4dev.com/employees.json')
			.success(function(data) {
				$scope.employees = data;
			});
	});

chapter05.html

	<script src="app/05/employee.js"></ script>

---

## Quiz 05-1

---

## Chapter 05 - End
