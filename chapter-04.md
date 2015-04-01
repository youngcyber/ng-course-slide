## Chapter 04 - CRUD Application

---

### File Structure

	chapter04.html
	app/
		04/
			app.js

---

### List Employees from JSON

app.js

	var app = angular.module('app', []);

	app.controller('EmployeeController', function($scope, $http) {

		$http.get('http://api-slim.tutor4dev.com/employees.json')
			.success(function(data) {
				$scope.employees = data;
			});
	});

chapter04.html

	<p ng-repeat="e in employees">
		{{ e.first_name }}
	</p>

---

### Delete Last Employee

app.js

	$scope.deleteEmployee = function() {
		$scope.employees.pop();
	}

chapter04.html

	<button ng-click="deleteEmployee()">Delete</button>

---

### Delete In-Line Employee

app.js

	$scope.deleteEmployee = function(index) {
		$scope.employees.splice(index, 1);
	}

chapter04.html

	<p ng-repeat="e in employees">
		{{ e.first_name }}

		<button ng-click="deleteEmployee($index)">Delete</button>
	</p>

---

## Quiz 04-1

---

### Edit Employee

app.js

	$scope.toggleEditMode = function() {
		$scope.editMode = !$scope.editMode;
	}

chapter04.html

	<p ng-repeat="e in employees">
		<span ng-show="!edit">
			{{ $index + 1 + ' ' + e.first_name }}
			<button ng-show="!editMode"
				ng-click="edit=true;toggleEditMode()">Edit
			</button>
		</span>

		<span ng-show="edit">
			<input type="text" ng-model="e.first_name">
			<button ng-click="edit=false;toggleEditMode()">Save</button>
		</span>
	</p>

---

## Chapter 04 - End
