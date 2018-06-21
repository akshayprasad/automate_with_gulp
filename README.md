<p align="center">
  <a href="http://gulpjs.com" rel="nofollow">
    <img src="https://raw.githubusercontent.com/gulpjs/artwork/master/gulp-2x.png" style="max-width:100%;" width="114" height="257">
  </a>
</p>

## What is gulp?
<p>gulp is a toolkit for automating painful or time-consuming tasks in your development workflow, so you can stop messing around and build something. </p>

## Features or Advantages:

<ul>
	<li><b>Simple Usage: </b> <p>By preferring code over configuration, node best practices, and a minimal API surface - gulp makes things simple like never before. </p></li>
	<li><b>Efficient Builds: </b> <p>Using the power of node streams, gulp gives you fast builds that don't write intermediary files to disk. </p></li>
	<li><b>Quality Ecosystem: </b> <p>By enforcing strict guidelines, we ensure our plugins stay simple and work as expected.  </p></li>
</ul>

## Can be done using gulp are:
<p>There are several key features regarding the use of Gulp which would make you want to use it. The one I hold as the most important is the way it can simulate the server environment where you will ultimately be hosting your code. This includes moving files around your project directory, and more importantly placing them in a <b>development directory</b> where you will be running a web server. Gulp also enables you to <b>compile</b>, <b>minify</b> and <b>concatenate</b> any files you want. All with the sole goal of getting your code base’s footprint down to the absolute minimum. In this process making it ready for moving to <b>production</b>. It’s perfectly fine if you don’t know any of the terms above, we’ll go through them in more detail a bit further down.</p>

## Key features:

<ol style="line-height: 2.5">
	<li>Three main Gulp commands: <b>gulp.task</b>, <b>gulp.src</b>, <b>gulp.dest</b>.</li>
	<li>The <b>pipe()</b> method is built into Node.js and is used to copy files from one folder to another.</li>
	<li>Have a logical folder structure, with three main folders. The <b>src</b> folder for pre-processed files, <b>tmp</b> for the local development server and <b>dist</b> for processed and minified files.</li>
	<li>Create separate tasks for pipeing HTML, CSS and JavaScript files from <b>src</b> to <b>tmp</b>.</li>
	<li>Combine the HTML, CSS and JavaScript tasks into one main <b>‘copy’</b> task. This will let you copy all the files with one command.</li>
	<li>After all files have been copied you want to reference them automatically in your main index.html. This is done with an ‘inject’ task and is called injecting dependencies.</li>
	<li>When the files have been copied and injected it’s time to run a development server on the tmp folder.</li>
	<li>While the server is running you <b>‘watch’</b> for changes, and enable live reloading on the local development server.</li>
	<li>If you feel code is fine, <b>'build'</b> the production files and place them in <b>dist</b> directory</li>
	<li>Delete tmp and dist before pushing to GitHub. (Or just add them to your .gitignore)</li>
</ol>


## Tools required:
<ol>
	<li> <b>Node</b> has to be installed in the user machine. 
			<p><b>node -v //Check in the command prompt.</b></p>
		<p>If not download from here: <a href="https://nodejs.org/en/download/"> Node download</a></p>
	</li>
	<li>
		Install gulp and type this command in the command prompt.
		<p><b>npm install -g gulp</b></p>
	</li>
</ol>

## steps to follow:

<p>As Gulp is a package on npm you will need to initialize <b>npm</b> to have a link to the package manager.</p>
<p>To know more about <b>npm — the Node Package Manager</b> please refer this link <a href="https://www.npmjs.com/">npm</a></p>

<p>Now you need to install the gulp locally, as it runs the local version in the project folders.</p>

```js
	npm init
	npm install gulp --save-dev
```

Installing it with the <b>--save-dev</b> flag will include it in the <b>package.json</b> beneath the development dependencies.

<p>Create a new file, name it <b>gulpfile.js</b>. This file is the entry point for Gulp, here’s where you will be writing all the code to automate tasks.</p>

```js
	Sample task:

	var gulp = require('gulp');

	gulp.task('default', function () {
  		console.log('This is gulp task!!!');
	});

	Run 'gulp default' in command prompt
	Check the console for the output
```


## Follow the structure:

<p>Create the <b>src</b> folder, but <b>do not</b> create the <b>dist nor the tmp</b> folder yet. You will see a bit further down how you can create it dynamically and incorporate it into an automated task. Let’s add some files to the src folder, to finally have something to play with. An <b>index.html</b>, a <b>script.js</b> and a <b>style.css</b> should be more than enough. These will serve as your source files, the only files you will be editing. Gulp will handle everything else.</p>


## Folder structure:

<p>First of all you need a <b>paths</b> variable to store all the file and directory paths of your project. Place this right under where you required gulp.</p>

```js

	// gulpfile.js
	var gulp = require('gulp');
	
	var paths = {
  		src: 'src/**/*',
  		srcHTML: 'src/**/*.html',
  		srcCSS: 'src/**/*.css',
  		srcJS: 'src/**/*.js',

  		tmp: 'tmp',
  		tmpIndex: 'tmp/index.html',
  		tmpCSS: 'tmp/**/*.css',
  		tmpJS: 'tmp/**/*.js',

  		dist: 'dist',
  		distIndex: 'dist/index.html',
  		distCSS: 'dist/**/*.css',
  		distJS: 'dist/**/*.js'
	};


```

## Set up the HTML task
<p>Now you need to create a task to copy all HTML files from the <b>src</b> directory to the <b>tmp</b> directory where you’ll be running the web server.</p>

```js

	gulp.task('html', function () {
  		return gulp.src(paths.srcHTML).pipe(gulp.dest(paths.tmp));
	});

```

##  Set up the CSS task
<p>Just a like html task we do it for css</p>

```js
	gulp.task('css', function () {
  		return gulp.src(paths.srcCSS).pipe(gulp.dest(paths.tmp));
	});
```

## Set up the JavaScript task

<p>Just a like html task we do it for js</p>

```js
	gulp.task('js', function () {
  		return gulp.src(paths.srcJS).pipe(gulp.dest(paths.tmp));
	});
```

## Combine all tasks into one task

<p>Gulp allows you to combine tasks, and add tasks to other tasks as dependencies. This feature is incredibly useful because you can tell Gulp to run and complete certain tasks before even starting other tasks.</p>

```js
	gulp.task('copy', ['html', 'css', 'js']);
```

### Important
<ul>
	<li>The <b>tmp</b> directory is created dynamically.</li>
	<li>The <b>tmp</b> directory contains the same files you have in the src directory. </li>
	<li>The <b>.pipe()</b> command has copied files from the source to the given destination.</li>
</ul>

## Inject files into the index.html
The inject task with <b>'copy'</b> dependency adds the css reference link to the index file of <b>tmp</b> and js reference link to the index file of <b>tmp</b>.

```js
	// Install the plugin to achieve the task
	npm install gulp-inject --save-dev

	//Add the plugin to the gulpfile.js
	var inject = require('gulp-inject');
```

<b>The task :</b>

```js
	
	gulp.task('inject', ['copy'], function(){
    	var css = gulp.src(paths.tmpCSS);
    	var js = gulp.src(paths.tmpJS);

    	return gulp.src(paths.tmpIndex)
    	.pipe(inject( css, { relative:true } ))
    	.pipe(inject( js, { relative:true } ))
    	.pipe(gulp.dest(paths.tmp));
	});
```

<p>You’ve added the <b>‘copy’</b> task as a dependency for the <b>‘inject’</b> task. Gulp will first copy all the files to the tmp directory, only then will it do the injecting. Let’s break this down. You’re placing the <b>gulp.src</b> of the files copied to the tmp folder into two respective variables. One for the CSS, the other for the JavaScript files. In the return statement you grab the <b>index.html</b> which has already been piped to <b>tmp</b> with the <b>‘copy’</b> task and <b>.pipe()</b> the <b>inject()</b> function with the variables where you placed the respective files from the tmp directory. The second parameter you pass to the inject() function is an options object. Here, <b>relative:true means that the file paths to be referenced in the index.html will be relative.</b></p>

Now look at the <b>index.html</b> of <b>tmp</b> folder. The links are added automatically in the index.html.

```js
	<!DOCTYPE html>
	<html>
	  <head>
	    <!-- tmp/index.html -->
	  
	    <!-- inject:css -->
	    <link rel="stylesheet" href="style.css">
	    <!-- endinject -->
	  </head>
	  <body>

	    <!-- inject:js -->
	    <script src="script.js"></script>
	    <!-- endinject -->
	  </body>
	</html>
```


## Serve the development web server

```js

	// To install gulp-webserver plugin
	npm install gulp-webserver --save-dev

```

<p>This is a Gulp plug-in which allows you to run a web server on your local machine.</p>

```js

	//require this in the top of gulpfile.js
	var webserver = require('gulp-webserver');

```

```js

	//Add the task in the gulpfile.js

	gulp.task('serve', ['inject'], function () {
  		return gulp.src(paths.tmp)
    		.pipe(webserver({
      			port: 3000,
      			livereload: true
    		}));
	});

```

<p>Once again you need to include a dependency. Here you want the <b>‘inject’</b> task to finish before running the web server. Simply reference the <b>tmp</b> directory and <b>.pipe()</b> it to the web server. The <b>gulp-webserver</b> plug-in takes an options object as a parameter. You will need to specify the port on which it will run, and tell the server to reload if it senses any changes. Once you get used to this. There’s no going back.</p>

### Add some lines of code to the files in the src directory. 

<b>index.html</b>

```js

<!DOCTYPE html>
<html>
  <head>
    <!-- inject:css -->
    <!-- endinject -->
  </head>
  <body>
    <div class="gulpBasic">This is gulp task!!!</div>

    <!-- inject:js -->
    <!-- endinject -->
  </body>
</html>

```

<b>style.css</b>

```js

.gulpBasic {
  color: red;
}

```

<b>script.js</b>

```js

console.log('This is gulp task!');

```


### Run the task with serve command

```js
	 
	 gulp serve

	 Access with 'localhost:3000'

```


## Watch for changes

<P>Watching for changes means Gulp will constantly be checking for changes among your files. You only have to specify which files it has to watch.</P>

```js

	gulp.task('watch', ['serve'], function () {
  		gulp.watch(paths.src, ['inject']);
	});

```

<p>The <b>‘watch’</b> task will first wait for the <b>‘serve’</b> task to finish, only then will it start the watching. You tell Gulp to watch the files in the <b>src</b> directory. If it senses any changes it will fire the <b>‘inject’</b> Gulp task. Now whenever you save the changes in any of the specified files, Gulp will fire the <b>‘inject’</b> task. You can even go ahead and link the <b>‘watch’</b> task to the default task.</p>

```js
	
	gulp.task('default', ['watch']);

```

## Building the dist

With the development environment up and running you’ve come to the point where you want to pack up your files to make them ready for production. Here’s where Gulp really flexes its muscles. Go ahead and install the following Gulp plug-ins.

```js

	npm install gulp-htmlclean --save-dev
	npm install gulp-clean-css --save-dev
	npm install gulp-concat --save-dev
	npm install gulp-uglify --save-dev

```

<p>And require them at the top of the <b>gulpfile.js</b>.</p>

```js

	var htmlclean = require('gulp-htmlclean');
	var cleanCSS = require('gulp-clean-css');
	var concat = require('gulp-concat');
	var uglify = require('gulp-uglify');

```

<p>You can now re-use the majority of the already written tasks to create the build tasks.</p>

```js

gulp.task('html:dist', function () {
  return gulp.src(paths.srcHTML)
    .pipe(htmlclean())
    .pipe(gulp.dest(paths.dist));
});

gulp.task('css:dist', function () {
  return gulp.src(paths.srcCSS)
    .pipe(concat('style.min.css'))
    .pipe(cleanCSS())
    .pipe(gulp.dest(paths.dist));
});

gulp.task('js:dist', function () {
  return gulp.src(paths.srcJS)
    .pipe(concat('script.min.js'))
    .pipe(uglify())
    .pipe(gulp.dest(paths.dist));
});

gulp.task('copy:dist', ['html:dist', 'css:dist', 'js:dist']);

gulp.task('inject:dist', ['copy:dist'], function () {
  var css = gulp.src(paths.distCSS);
  var js = gulp.src(paths.distJS);
  return gulp.src(paths.distIndex)
    .pipe(inject( css, { relative:true } ))
    .pipe(inject( js, { relative:true } ))
    .pipe(gulp.dest(paths.dist));
});

gulp.task('build', ['inject:dist']);

```

The added plug-ins are piped between the <b>gulp.src</b> and <b>gulp.dest</b> commands. Everything else remains the same.

```js

<!DOCTYPE html>
<html>
  <head>
    <!--[htmlclean-protect]-->
    <!-- inject:css -->
    <!-- endinject -->
    <!--[/htmlclean-protect]-->
  </head>
  <body>
    <div class="gulpBasic">This is gulp task!!!</div>

    <!--[htmlclean-protect]-->
    <!-- inject:js -->
    <!-- endinject -->
    <!--[/htmlclean-protect]-->
</body>
</html>

```

<p>run the <b>‘build’</b> task.</p>

```js

	gulp build

```

Take a look at your project folder. You can now see a <b>dist</b> folder. The files within have been concatenated and minified.


## Cleaning up

It’s not considered good practice to pass the <b>tmp</b> and <b>dist</b> folders to GitHub or any version control. 
You will need a way to delete them without any problem.

```js

	npm install del --save-dev

	//Add the plugin to the gulpfile.hs
	var del = require('del');

	//And add this snippet of code in gulpfile.js
	gulp.task('clean', function () {
  		del([paths.tmp, paths.dist]);
	});

```

<p>The <b>tmp</b> and <b>dist</b> folders have been deleted!</p>

<p>Another good practice is to add the <b>tmp</b> and <b>dist</b> files path in the <b>.gitignore</b> file.</p>

