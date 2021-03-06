# Amateur Radio Club at Ohio State

[![Built with Grunt](https://cdn.gruntjs.com/builtwith.png)](http://gruntjs.com/)

A website for the Amateur Radio Club at The Ohio State University.

## Requirements

  * [Node.js](http://nodejs.org)
  * [bower](http://bower.io): `npm install -g bower`
  * [grunt](http://gruntjs.com): `npm install -g grunt-cli`

## Quickstart

To start the server for the first time or after any updates, just run the
following commands:

````bash
git submodule update --init
npm install
node server
````

You will then be able to access the project at http://localhost:3000/

To start the server subsequent times just run:

````bash
node server
````

## Upgrading

### Foundation

If you'd like to upgrade to a newer version of Foundation down the road just run:

```bash
bower update
```
### Node Libraries

If you'd like to update the libraries for the project run:

````bash
npm update --save
````

### Update Submodules

Git submodules are located in the `/vendor` directory. To update them all run

````bash
git submodule update --remote --merge
````

To update only one of them

````bash
cd vendor/$(submodule)
git pull
cd ../..
git commit -am "Updated submodule: $(submodule)"
````

## Development

### Creating new views

New views are created by creating a new route. This is done in the routes
directory. All files in the routes directory are loaded by `/routes/index.js`.
The routes for the public site are located in `/routes/root.js`. All
sub-sections of the site should be located in a separate route file similar to
`root.js`.

An example route file is located below, however, much more complex routes can be
created using express.

````js
// routes/foo.js
module.exports = function(app) {
  app.get('/foo', function (req, res) {
    res.render('foo', { title: 'Foo' });
    res.end();
  });
}
````

Then, you must create a new view file. All view files are created using the
[jade](http://jade-lang.com/) template language. This markup language is
compiled to html before being sent to the user.

New files should be created in `/views` and should extend the file layout.jade
unless they must use a different style from the rest of the website. These new
views should start like

````jade
extend layout
block content
````

From there, the content should be included.

#### Partials in jade

jade supports partials through two different methods. One is escaped partials

````jade
#{variable}
````

The other is an unescaped partial

````jade
!{variable}
````

### Modifying stylesheets

When working with style sheets, it may be convenient to run the default grunt
task. This task takes advantage of `grunt-contrib-watch` to recompile CSS
whenever the SASS sources are changed. All changes to the style sheets should be
made in the files located in `/scss`.

To run the default grunt task, which uglifies vendor javascript and creates the
CSS files, run

````bash
grunt
````

If you would rather just build only the CSS for updating the repository with, then
you should run

````bash
grunt build-css
````

This should only be done when you are done modifiying the stylesheets for the
current options.

### Updating Foundation and Other Javascript Providers

Whenever the javascript from vendors is updated via

````bash
bower update
````

It is require that you either run

````bash
grunt
````

Or

````bash
grunt build-js
````

To update the site's uglified copies of the javascript libraries.

### Developing nodejs files without restarting the server

To develop nodejs files without restarting the server, it is reccomended that
you use [nodemon](https://www.npmjs.org/package/nodemon). You can install
nodemon by running

````bash
npm install -g nodemon
````

nodemon is used in a similar fashion to running a node server. To run the
node server with nodemon run

````bash
nodemon server
````

Whenever you save a change to one of the javascript files in the directory,
nodemon will automatically restart the server for you. This way, you do not have
to manually restart the server.

While this is not a required development tool, it is recommended when actively
developing new routes especially when making small changes. Documentation on how
to use nodemon more effectively can be found at
https://github.com/remy/nodemon#nodemon.
