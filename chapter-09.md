## Chapter 09 - `$http`

---

### File Structure

	chapter09.html
	app/
		09/
			app.js
			views/
				employee.html
				employee_detail.html
				employee_create.html
				home.html

---

### `$http`

	$http({
		method: 'GET',
		url: 'http://api-php.tutor4dev.com/select.php',
		params: { 'emp_no': 101 }
	});

	$http({
		method: 'POST',
		url: 'http://api-php.tutor4dev.com/insert.php',
		data: {
			'emp_no': 101,
			'first_name': 'James',
			'last_name': 'Bond'
		}
	});

---

### `$http` Shorthand

	$http.get('http://api-php.tutor4dev.com/select.php?emp_no=101');

	$http.post('http://api-php.tutor4dev.com/select.php?emp_no=101', {
		'emp_no': 101,
		'first_name': 'James',
		'last_name': 'Bond'
	});

---

### Promise using `$q`

	app.factory('employeeFactory', function($http, $q) {
		var defer = $q.defer();

		$http.get(url)
			.success(function(data) {
				defer.resolve(data);
			});

		return defer.promise;
	});

---

### URI

- *GET* -> *http://api-php.tutor4dev.com/select.php*
- *GET* -> *http://api-php.tutor4dev.com/select.php?emp_no=101*
- *POST* -> *http://api-php.tutor4dev.com/insert.php*
- *POST* -> *http://api-php.tutor4dev.com/update.php*
- *POST* -> *http://api-php.tutor4dev.com/delete.php*

---

### Project Setup

app.js

	var app = angular.module('app', ['ngRoute']);

	app.constant('apiUrl', '//api-php.tutor4dev.com')

	app.config(function($routeProvider) {
		$routeProvider
			.otherwise({
				redirectTo: '/'
			})
	});

---

### Project Setup (2)

chapter09.html

	<a href="#/">Home</a> |
	<a href="#/employee">Employee</a> |
	<a href="#/create">Create</a>

	<div ng-view></div>

	<script src="js/angular.min.js"></ script>
	<script src="js/angular-route.min.js"></ script>
	<script src="app/09/app.js"></ script>

---

### Home Page

app.js

	.when('/', {
		controller: 'HomeController',
		templateUrl: 'app/09/views/home.html'
	})

	app.controller('HomeController', function() {});

home.html

	<h3>Home</h3>

---

### List Employees

app.js

	.when('/employee', {
		controller: 'EmployeeController',
		templateUrl: 'app/09/views/employee.html'
	})

---

### List Employees (2)

app.js

	app.factory('employeeFactory', function($http, $q, apiUrl) {
		return {
			listEmployees: function() {
				var defer = $q.defer();

				$http.get(apiUrl + '/select.php')
					.success(function(data) {
						defer.resolve(data);
					})
					.error(function() {
						defer.reject('Error ...');
					});
				return defer.promise;
			}
		};
	});

---

### List Employees (3)

	app.controller('EmployeeController',
		function($scope, employeeFactory) {

		$scope.employees = [];

		employeeFactory.listEmployees()
			.then(function(data) {
				$scope.employees = data;
			}, function() {
				console.log('Error ...');
			});
	});

---

### List Employees (4)

employee.html

	<h3>Employee</h3>

	<p ng-repeat="e in employees">
		<a href="#/employee/{{e.emp_no}}">{{ e.emp_no }}</a>
		{{ e.first_name + ' ' + e.last_name }}
	</p>

---

### Delete Employee

app.js

	app.factory('employeeFactory', function($http, $q, apiUrl) {
		return {
			deleteEmployee: function(id) {
				var defer = $q.defer();

				$http.post(apiUrl + '/delete.php', {'emp_no': id})
					.success(function(data) {
						defer.resolve(data);
					})
					.error(function() {
						defer.reject('Error ...');
					});
				return defer.promise;
			}
		};
	});

---

### Delete Employee (2)

app.js

	app.controller('EmployeeController',
		function($scope, employeeFactory) {

		$scope.deleteEmployee = function(id) {
			employeeFactory.deleteEmployee(id)
				.then(function() {
					console.log('Success');
				});
		}
	});

employee.html

	<input type="button" value="Delete"
		ng-click="deleteEmployee(e.emp_no)">

---

### Employee Detail

app.js

	.when('/employee/:id', {
		controller: 'EmployeeDetailController',
		templateUrl: 'app/09/views/employee_detail.html'
	})

---

### Employee Detail (2)

app.js

	app.factory('employeeFactory', function($http, $q, apiUrl) {
		return {
			showEmployee: function(id) {
				var defer = $q.defer();
				$http.get(apiUrl+'/select.php?emp_no='+id,{'emp_no':id})
					.success(function(data) {
						defer.resolve(data);
					})
					.error(function() {
						defer.reject('Error ...');
					});
				return defer.promise;
			}
		};
	});

---

### Employee Detail (3)

app.js

	app.controller('EmployeeDetailController',
		function($scope, $routeParams, employeeFactory) {

		$scope.employee = {};

		employeeFactory.showEmployee($routeParams.id)
			.then(function(data) {
				$scope.employee = data;
				$scope.employee.old_emp_no = $scope.employee.emp_no;
			});
	});

---

### Employee Detail (4)

employee_detail.html

	<h3>Employee Detail</h3>

	<p>Employee #<input type="text" ng-model="employee.emp_no"></p>
	<p>First Name<input type="text" ng-model="employee.first_name"></p>
	<p>Last Name<input type="text" ng-model="employee.last_name"></p>

---

### Update Employee

app.js

	app.factory('employeeFactory', function($http, $q, apiUrl) {
		return {
			updateEmployee: function(employee) {
				var defer = $q.defer();

				$http.post(apiUrl + '/update.php', employee)
					.success(function(data) {
						defer.resolve(data);
					})
					.error(function() {
						defer.reject('Error ...');
					});
				return defer.promise;
			}
		};
	});

---

### Update Employee (2)

app.js

	app.controller('EmployeeDetailController',
		function($scope, $routeParams, employeeFactory) {

		$scope.updateEmployee = function() {
			employeeFactory.updateEmployee($scope.employee);
		}
	});

employee_detail.html

	<p><input type="button" value="Update"
		ng-click="updateEmployee()"></p>

---

### Create Employee

app.js

	.when('/create', {
		controller: 'EmployeeCreateController',
		templateUrl: 'app/09/views/employee_create.html'
	})

---

### Create Employee (2)

app.js

	app.factory('employeeFactory', function($http, $q, apiUrl) {
		return {
			createEmployee: function(employee) {
				var defer = $q.defer();

				$http.post(apiUrl + '/insert.php', employee)
					.success(function(data) {
						defer.resolve(data);
					})
					.error(function() {
						defer.reject('Error ...');
					});
				return defer.promise;
			}
		};
	});

---

### New Employee (3)

app.js

	app.controller('EmployeeCreateController',
		function($scope, $location, employeeFactory) {

		$scope.createEmployee = function() {
			employeeFactory.createEmployee($scope.employee)
				.then(function() {
					$location.path('/employee');
				});
		}
	});

---

### New Employee (4)

employee_create.html

	<h3>New Employee</h3>

	<p>Employee #<input type="text" ng-model="employee.emp_no"></p>
	<p>First Name<input type="text" ng-model="employee.first_name"></p>
	<p>Last Name<input type="text" ng-model="employee.last_name"></p>

	<p><input type="button" value="Save"
		ng-click="createEmployee()">
	</p>

---

## Chapter 09 - End