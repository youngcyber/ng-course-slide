### Chapter 01 - JavaScript

	<body>
		<script>
			//code here
		</ script>
	</ body>

---

### Chrome's Developer Tool

![](http://i.cubeupload.com/ikYxC6.png)

---

### Variables Declaration

	var v1;

	var v2 = 'Hello, World';

	console.log(v2);

---

### Functions Declaration

	function hello() {
		console.log('Hello');
	}

	function hello(param) {
		console.log('Hello ' + param);
	}

---

### Operators

	var v1 = 10;

	if (v1 == 10) {
		console.log('Equal to 10');
	} else {
		console.log('No equal to 10')
	}

---

### Array

	var a1 = [1, 2, 3, 4];
	var a2 = ['A', 'B', 'C'];

	console.log(a1);
	console.log(a1[0]);

---

### Object

	var o1 = {};

	var o2 = {
		name: 'Chai',
		age: 35,
		birthdate: new Date()
	};

	console.log(o2);
	console.log(o2.name);
	console.log(JSON.stringify(o2));

---

### Object with Functions

	var o3 = {
		name: 'Chai',
		greet: function() {
			console.log('Hello');
		}
	}

	o3.greet();

---

### Array of Objects

	var ao1 = [ {} ];

	var ao2 = [
		{
			name: 'Chai',
			age: 35
		},
		{
			name: 'Sak',
			age: 28
		}
	];

	console.log(ao2);

---

### JSON (JavaScript Object Notation)

	var ao = [
		{
			name: 'Chai',
			age: 35
		},
		{
			name: 'Peter',
			age: 42
		}
	];

	console.log(ao);
	//array of object to JSON
	console.log(JSON.stringify(ao));

---

### JSON (JavaScript Object Notation)

	var j = '{"name":"Chai","age":35,"birthdate":"2015-03-23"}';

	console.log(j);
	//JSON to object
	console.log(JSON.parse(j));

---

## Chapter 01 - End
