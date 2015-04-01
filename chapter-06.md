## Chapter 06 - Single Page Appliation

---

### File Structure

	chapter06.html
	app/
		06/
			app.js
			views/
				home.html
				about.html
				employee.html
				employee_detail.html

---

### Single Page Application

chapter06.html

	<body>
		<a href="#/">Home</a> | <a href="#/about">About</a>

		<div ng-view></div>

		<script src="angular.min.js"></ script>
		<script src="angular-route.min.js"></ script>

		<script src="app/06/app.js"></ script>
	</ body>

---

### Single Page Application (2)

home.html

	<h3>Home</h3>

	<p>{{ controllerName }}</p>

about.html

	<h3>About</h3>

	<p>{{ controllerName }}</p>

---

### Single Page Application (3)

app.js

	var app = angular.module('app', ['ngRoute']);

	app.controller('HomeController', function($scope) {
		$scope.controllerName = 'This is HomeController';
	});

	app.controller('AboutController', function($scope) {
		$scope.controllerName = 'This is AboutController';
	});

---

### Single Page Application (4)

app.js

	app.config(function($routeProvider) {
		$routeProvider
			.when('/', {
				controller: 'HomeController',
				templateUrl: 'app/06/views/home.html'
			})
			.when('/about', {
				controller: 'AboutController',
				templateUrl: 'app/06/views/about.html'
			})
			.otherwise({
				redirectTo: '/'
			})
	});

---

## Quiz 06-1

---

### Parameterized Route

app.js : `config()`

	.when('/employee/:id', {
		controller: 'EmployeeDetailController',
		templateUrl: 'app/06/views/employee_detail.html'
	})

app.js : `EmployeeDetailController`

	app.controller('EmployeeDetailController',
		function($scope, $routeParams, $http) {

		$scope.id = $routeParams.id;

		$scope.query = {
			emp_no: $scope.id
		};

		$http.get('employees.json')
			.success(function(data) {
				$scope.employees = data;
			});
	});

---

### Parameterized Route (2)

employee_detail.html

	<h3>Employee Detail</h3>

	Employee ID: {{ id }}

	{{ query }}

	<p ng-repeat="e in employees | filter: query">
		Name: {{ e.first_name + ' ' + e.last_name }}
		<br>
		Gender: {{ e.gender }}
	</p>

---

## Quiz 06-2

---

## Chapter 06 - End
