## Getting Started

![](http://i.cubeupload.com/HNiXf4.jpg)

---

### Instructor

Kongthap Thammachat (tutor4dev)

Line ID: jeud

Facebook: Kongthap Thammachat

---

### jQuery

- DOM
- AJAX

---

### Why AngularJS

- DOM
- AJAX
- MVC
- Modularized
- Depedency Injection
- Unit Testing

---

### AJAX

![](http://i.cubeupload.com/c5F2FE.jpg)

---

## SETUP

---

### Sublime Package Control

![](http://i.cubeupload.com/aZmNsp.png)

Sublime -> View -> Show Console

---

### Sublime Packages

- *HTML5*
- *SublimeCodeIntel*
- *AngularJS*
- *AngularJS Snippets*

---

### Ecosystem

- `gulp`
- `gulp-connect`
- `livereload`

---

### Ecosystem Setup

	ng-course/
		package.json
		gulpfile.js
		index.html

---

### package.json

	{
		"dependencies": {},
		"devDependencies": {
			"gulp": "latest",
			"gulp-connect": "latest"
		}
	}

---

### gulpfile.js

	var
		src = [
			'*.html',
			'*.js',
			'app/**/*.html',
			'app/**/*.js'
		];

---

### Ecosystem Installation

	npm install -g gulp

	npm install

	gulp

---

### index.html

	<!DOCTYPE html>
	<html>
	<head>
		<title>AngularJS - Course</title>
	</head>

	<body>
		<h3>AngularJS - Course</h3>
	</body>
	</html>

---

### Launch Project

	http://localhost:8000

---

### Project Folder Setup

	ng-course/
		chapter_xx.html
		app/
			xx/
				app.js

---

## END - Introduction