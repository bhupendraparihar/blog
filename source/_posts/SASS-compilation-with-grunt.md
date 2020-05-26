---
title: SASS compilation with grunt
date: 2020-05-22 12:27:02
tags:
---
When SASS file is compiled, you get .CSS file. I am not going to explain the syntax of SASS, instead of that I will explain how it is setup with grunt so that you can compile the SASS file easily.

Prerequisite for SASS
<ol>
	<li>Node js installed</li>
	<li>grunt installed</li>
</ol>
Now go to the specific folder where you want to setup your web project
and install grunt-contrib-sass package. There are many ways to do that. Simplest one is running command in your terminal or command prompt.
<pre>npm install grunt-contrib-sass</pre>
This will download grunt-contrib-sass package in your node_modules folder. Another way of install this package is by including dependencies in package.json file.

Create a simple html file where you can apply your generated stylesheet(.css).

Now create a sample .sass file called style.sass
<pre>
$primary-color: #FCF

body
  color: $primary-color
</pre>
Once you done with that you need to create grunt file named GruntFile.js and write the below code in that file.
<pre>module.exports = function(grunt) {

grunt.initConfig({
  sass: {                              // Task
    dist: {                            // Target
      options: {                       // Target options
        style: 'expanded'
      },
      files: {                         // Dictionary of files
        'style.css': 'style.sass'       // 'destination': 'source'
      }
    }
  }
});

grunt.loadNpmTasks('grunt-contrib-sass');

grunt.registerTask('default', ['sass']);

};
</pre>
now run the below command in your terminal
<pre>grunt</pre>
This command will compile your style.sass file into style.css. You can see the directory for newly created file, which will look like
<pre>body {
  color: #ffccff;
}</pre>
Open your index.html file which you have created earlier by following this tutorial.