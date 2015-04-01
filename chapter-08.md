## Chapter 08 - `$resource`

---

### File Structure

	chapter08.html
	app/
		08/
			app.js

---

### URI

- *GET* -> *http://api-slim.tutor4dev.com*
- *GET* -> *http://api-slim.tutor4dev.com/:id*
- *POST* -> *http://api-slim.tutor4dev.com*
- *PUT* -> *http://api-slim.tutor4dev.com/:id*
- *DELETE* -> *http://api-slim.tutor4dev.com/:id*

---

### Setup `$resource`

app.js

	var app = angular.module('app', ['ngResource']);

	app.constant('apiUrl', '//api-slim.tutor4dev.com');

	app.factory('EmployeeFactory', function($resource, apiUrl) {

		return $resource(apiUrl + '/employee/:id');

	});

---

### Setup `$resource` (2)

chapter08.html

	<script src="angular.min.js"></ script>
	<script src="angular-resource.min.js"></ script>

	<script src="app/08/app.js"></ script>

---

### List Employees

app.js

	app.controller('ListController', function($scope, EmployeeFactory) {

		$scope.employees = EmployeeFactory.query();
	});

chapter08.html

	<p ng-repeat="e in employees">
		{{ e.emp_no + ': ' + e.first_name + ' ' + e.last_name }}
	</p>

---

### Employee Detail

app.js

	app.controller('ShowController', function($scope, EmployeeFactory) {

		$scope.showEmployee = function() {
			$scope.employee = EmployeeFactory.get({id: $scope.emp_no});
		}
	});

chapter08.html

	<div ng-controller="ShowController">
		Employee #: <input type="text" ng-model="emp_no">

		<input type="button" ng-click="showEmployee()" value="Show">
		<p>{{ employee.first_name + ' ' + employee.last_name }}</p>
	</div>

---

### New Employee

app.js

	app.controller('CreateController',
		function($scope, EmployeeFactory) {

		$scope.createEmployee = function() {
			var postData = {
				emp_no: $scope.employee.emp_no,
				first_name: $scope.employee.first_name,
				last_name: $scope.employee.last_name
			};

			EmployeeFactory.save(postData);
		}
	});

---

### New Employee (2)

chapter08.html

	<div ng-controller="CreateController">
		<input type="text" ng-model="employee.emp_no">
		<input type="text" ng-model="employee.first_name">
		<input type="text" ng-model="employee.last_name">

		<input type="button" ng-click="createEmployee()" value="Create">
	</div>

---

### Delete Employee

app.js

	app.factory('EmployeeFactory', function($resource, apiUrl) {

		return $resource(
			apiUrl + '/resource/employee/:id', {}, {
				delete: {
					headers: { 'X-HTTP-Method-Override': 'DELETE' }
				}
			}
		);
	});
	app.controller('DeleteController',
		function($scope, EmployeeFactory) {
		$scope.deleteEmployee = function() {
			EmployeeFactory.delete({ id: $scope.emp_no });
		}
	});

---

### Delete Employee (2)

chapter08.html

	<div ng-controller="DeleteController">
		<input type="text" ng-model="emp_no">

		<input type="button" ng-click="deleteEmployee()" value="Delete">
	</div>

---

### Edit Employee

app.js

	app.factory('EmployeeFactory', function($resource, apiUrl) {

		return $resource(
			apiUrl + '/resource/employee/:id', {}, {
				update: {
					method: 'PUT',
					isArray: false,
					params: { id: '@id' },
					headers: { 'X-HTTP-Method-Override': 'PUT' }
				}
			}
		);
	});

---

### Edit Employee (2)

app.js

	app.controller('UpdateController',
		function($scope, EmployeeFactory) {

		$scope.updateEmployee = function() {
			var postData = {
				emp_no: $scope.employee.emp_no,
				first_name: $scope.employee.first_name,
				last_name: $scope.employee.last_name
			};
			EmployeeFactory.update({
				id: $scope.old_emp_no
			}, postData);
		}
	});

---

### Edit Employee (3)

chapter08.html

	<div ng-controller="UpdateController">
		<input type="text" ng-model="old_emp_no">

		<input type="text" ng-model="employee.emp_no">
		<input type="text" ng-model="employee.first_name">
		<input type="text" ng-model="employee.last_name">

		<input type="button" ng-click="updateEmployee()" value="Update">
	</div>

---

## Chapter 08 - End
