## gulp

---

### Install Plugin

	npm install gulp-concat

	npm install gulp-uglify gulp-cssmin

---

### Install Plugin + Update package.json

	npm install gulp-concat --save

	npm install gulp-uglify --save-dev

---

### Remove Plugin

	npm remove gulp-concat

	npm remove gulp-concat --save-dev

---

### Remove Plugin

Update *package.json*

	npm prune

### gulpfile.js

	var
		gulp = require('gulp'),
		connect = require('gulp-connect'),
		concat = require('gulp-concat');

---

### gulp Task

*gulpfile.js*

	gulp.task('hello', function() {
		console.log('Hello World');
	});

Terminal

	gulp hello

---

### Default Task

*gulpfile.js*

	gulp.task('default', function() {
		console.log('This is default task');
	});

Terminal

	gulp

---

### Default Task (2)

	gulp.task('default', ['hello']);

	gulp.task('default', ['hello', 'uglify']);

---

### concat

	var concat = require('gulp-concat');

	gulp.task('concat', function() {
		gulp.src('*.js')
			.pipe(concat('newfile.js'))
			.pipe(gulp.dest(__dirname));
	});

---

### `gulp.src()`

	gulp.src('filename');
	gulp.src(['file1', 'file2']);

	var paths = ['file1', 'file2'];
	gulp.src(paths);

---

### `gulp.src()` (2)

	var	paths = {
		src: [
			'*.html',
			'app/**/*.html',
			'app/**/*.js'
		],
		dest: __dirname
	}

	gulp.task('concat', function() {
		gulp.src(paths.src)
			.pipe(concat('newfile.js'))
			.pipe(gulp.dest(paths.dest));
	});

---

### `uglify()`

	var uglify = require('gulp-uglify');

	gulp.task('concat', function() {
		gulp.src(paths.src)
			.pipe(concat('newfile.min.js'))
			.pipe(uglify())
			.pipe(gulp.dest(paths.dest));
	});

---

### Quiz 01

*chapter07.html*

	gulp.task('concat', function() {
		gulp.src('???')
			.pipe(concat('concat.js'))
			.pipe(gulp.dest('???'));
	});

---

### `watch()`

*gulpfile.js*

	gulp.task('watch', function() {
		gulp.watch('app/07/*.js', ['concat']);
		gulp.watch(src, ['reload']);
	});

*chapter07.html*

	<script src="app/07/concat/concat.js"></script>

---

### `cssmin()`

	var cssmin = require('gulp-cssmin');
	var rename = require('gulp-rename');

	gulp.task('cssmin', function() {
		gulp.src('*.css')
			.pipe(cssmin())
			.pipe(rename({suffix: '.min'}))
			.pipe(gulp.desc('css/'));
	});

---

### `autoprefixer()`

	var autoprefixer = require('gulp-autoprefixer');

	var
		browsers = [
			'ie >= 7',
			'ff >= 26',
			'chrome >= 30',
			'safari >= 3',
		];

	gulp.task('autoprefixer', function() {
		gulp.src('dev.css')
			.pipe(autoprefixer(browsers))
			.pipe(rename('production.css'))
			.pipe(gulp.dest(__dirname));
	});

---

### `autoprefixer()` (2)

*dev.css*

	div {
		transition: width 2s;
		transition-delay: 1s;
	}

---

### Quiz 02

`autoprefixer()` + `cssmin()` + `watch()`

---

### `image-optimization()`

	var imgOpz = require('gulp-image-optimization');

	gulp.task('images', function(callback) {
		gulp.src(['src/*.png','src/*.jpg'])
			.pipe(imgOpz({
				optimizationLevel: 5,
				progressive: true,
				interlaced: true
			}))
			.pipe(gulp.dest('images/'))
			.on('end', callback)
			.on('error', callback);
	});

---

### `vinyl-ftp()`

	var ftp = require('vinyl-ftp');
	var util = require('gulp-util');

	var ftpCnt = ftp.create({
        host: 'ftp.xxx.com',
        user: 'xxx',
        password: 'yyy',
        parallel: 10,
        log: util.log
    });

	gulp.task('ftp', function() {
		gulp.src('*.*')
	        .pipe(ftpCnt.newer('/public_html'))
	        .pipe(ftpCnt.dest('/public_html'));
	});

---

## End - gulp