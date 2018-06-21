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

<p>Create a new file, name it <p>gulpfile.js</p>. This file is the entry point for Gulp, here’s where you will be writing all the code to automate tasks.</p>

```js
	Sample task:

	var gulp = require('gulp');

	gulp.task('default', function () {
  		console.log('This is gulp task!!!');
	});

	Check the console for the output
```