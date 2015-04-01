## Getting Started using AngularJS

---

### Instructor

Kongthap Thammachat (tutor4dev)

Line ID: jeud

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

## END