### Chapter 02 - AngularJS

	<html ng-app>

	<body>
		<script src="angular.min.js">
		</ script>
	</ body>

	</ html>

---

### Hello World

	<html ng-app>

	<body>

		{{ 'Hello World' }}
		<br>
		{{ 10 + 20 }}

		<script src="angular.min.js">
		</ script>
	</ body>

	</ html>

---

### Directive `ng-init`

	<body ng-init="price=500;qty=40">

		Amount: {{ price * qty }}

	</ body>

---

### Directive in AngularJS

- `ng-init`
- `ng:init`
- `ng_init`
- `x-ng-init`
- `data-ng-init`

---

### Expression `{{ }}` And `ng-bind`

Expression and Basic Filter

	{{ 1500 | currency }}

`ng-bind`

	<span ng-bind="price | currency:'THB '"></span>
	<br>
	<span ng-bind="qty"></span>

---

### Directive `ng-model`

`ng-model` with `<input type="text">`

	<input type="text" ng-model="name">

	<h3>Hello, {{ name }}</h3>

---

### Directive `ng-model`

`ng-model` with `<input type="radio">`

	Do you like this ?
	<br>
	<input type="radio" value="Yes" ng-model="like"> Yes
	<br>
	<input type="radio" value="No" ng-model="like"> No
	<br>
	You answer: {{ like }}

---

### Directive `ng-model`

`ng-model` with `<select>`

	<select ng-model="age">
		<option value="So Young">Less than 18</option>
		<option value="Young">18 - 25</option>
		<option value="Mature">26 - 30</option>
		<option value="Old">Greater 30</option>
	</select>
	<br>
	You are: {{ age }}

---

### Directive `ng-change`

	<input type="text" ng-change="counter=counter+1" ng-model="text">

	{{ counter }}

---

### Directive `ng-show`, `ng-hide`

	<body ng-init="show=true">

		<h3>Value of <i>show</i>: {{ show }}</h3>

		<h3 ng-show="show" style="background-color: red;">Show</h3>
		<h3 ng-hide="show" style="background-color: green;">Hidden</h3>

	</ body>

---

### Directive `ng-click`

Toggle

	<button ng-click="show=!show">Toggle</button>

Increment

	<button ng-click="counter=counter+1">Counter</button>

	<h3>{{ counter }}</h3>

---

### Directive `ng-if`

	<h3 ng-if="show" style="background-color: red;">Show</h3>

	<h3 ng-if="!show" style="background-color: green;">Hidden</h3>

---

### Directive `ng-switch`

	<input type="radio" ng-model="color" value="red"> Red
	<input type="radio" ng-model="color" value="blue"> Blue
	<input type="radio" ng-model="color" value="green"> Green
	<input type="radio" ng-model="color" value="pink"> Pink

	<div ng-switch="color">
		<span ng-switch-when="red" style="color: {{color}};">Red</span>
		<span ng-switch-when="blue" style="color: {{color}};">Blue</span>
		<span ng-switch-when="green" style="color: {{color}};">Green</span>
		<span ng-switch-default>Others</span>
	</div>

---

### Directive `ng-class`

Style

	<style>
		.italic { font-style: italic }

		.bold { font-weight: bold; }
	</style>

`ng-class`

	<input type="checkbox" ng-model="s1" ng-true-value="'bold'">Bold
	<input type="checkbox" ng-model="s2" ng-true-value="'italic'">Italic

	<p ng-class="[s1, s2]">Hello, World</p>

---

## Chapter 02 - End
