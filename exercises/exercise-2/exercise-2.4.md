# Exercise 2.4 \(Optional\)

### Implement Sass workflow

Pattern Lab out of the box provides a basic workflow for compiling CSS for components. Unfortunately this is not an optimal way to manage CSS assets in a project. It requires repetitive manual steps every time a new CSS file is created for a component. We are going to implement a simple automated workflow to achieve two goals:

1. Write a component's CSS/Sass within the component's directory.  This way each component will contain styles only intended for the component
2. Combine all compiled CSS into a single stylesheet to automate Pattern Lab's styling of components in the browser. This will solve Pattern Lab's process to manually add each new stylesheet by hand

#### Our new workflow will need the following:

* Add Gulp and its dependencies to our project.  Gulp is a task runner to automate slow, repetitive tasks such as compile Sass code into CSS.
* Change location of source CSS code to **\_patterns**.  By default Pattern Lab uses the CSS directory for storing CSS files, but we want to be able to create Sass files directly within the component's directories.
* Ensure our CSS code complies with standards and best practices by using a code linter to check the code's integrity.  This is extremely helpful as it will warn you if the code you are writing needs improvements.

This will be as basic of a workflow as it gets but will make it possible to use Sass instead of plain CSS. Let's start.

### Add Gulp and other node dependencies

{% hint style="info" %}
Learn more about [Gulp](https://gulpjs.com/).
{% endhint %}

1. In your code editor open `package.json`, which is located in the root of your project
2. Scroll to the bottom of the file until you get to the `dependencies` section
3. Add the following code directly after the last item \(`"@pattern-lab/uikit-workshop"`

   `: “^x.x.x”`\), where x is the version number.

4. Then **save** your changes.

{% hint style="warning" %}
**IMPORTANT:**  Since this is JSON, be sure you add a comma after `“@pattern-lab/uikit-workshop”: “^x.x.x”`\(where x is the version number\).  No comma is needed in the last item you will be adding.  In addition, ensure the indentation of the new code below matches the rest of the file's indentation.
{% endhint %}

{% tabs %}
{% tab title="package.json" %}
```javascript
"gulp": "^4.0.2",
"gulp-autoprefixer": "^7.0.1",
"gulp-changed": "^4.0.2",
"gulp-concat": "^2.6.1",
"gulp-order": "^1.2.0",
"gulp-rename": "^1.4.0",
"gulp-sass": "^4.0.2",
"gulp-stylelint": "^11.0.0",
"stylelint": "^12.0.1",
"stylelint-scss": "^3.13.0"
```
{% endtab %}
{% endtabs %}

* The above are node dependencies we need in order for Gulp to run our tasks.  If you want to learn more about what each dependency is for you can look them up.

#### Adding new commands for compiling and watching Sass file

1. While still ins `package.json` scroll to the top and add the following code into the `scripts` section:

{% tabs %}
{% tab title="package.json" %}
```yaml
"gulp": "gulp",
"watch": "gulp watch",
"lint": "gulp lint"
```
{% endtab %}
{% endtabs %}

* The 3 lines of code above should be added directly after the last item in the scripts section \(`"version": "patternlab --version"`\).
* Be sure to add a comma on that last item prior to adding the lines above.

#### Installing the dependencies

The way most modern web development projects work nowadays is by having a file that keeps tracks of plugins and dependencies to perform the various tasks in our project.  This is not unique to Pattern Lab.  In our case that file is `package.json`.  This file ensures everyone working on this project uses the same tools and versions so there is a consistent experience among team members working on the same project.  The next step is to actually install all the dependencies in our project.

1. If you have Pattern Lab running in your command line, stop it by pressing **Ctrl + C** in your keyboard \(Mac & Windows\), then pressing **Return.**  Sometimes you may need to do this more than once for the current job to stop.
2. Next type `npm install` and press **Return**.  This command will look in `package.json` and will install all the plugins we added above.  This can take a few minutes to complete.  Do not interrupt it.

{% hint style="warning" %}
**READ THIS:**  You may notice errors and warning messages on your screen.  As long as the installation of plugins keeps running you can ignore them.  If an error occurs and the installation job stops, then we have a problem.  [See our troubleshooting guide](https://docs.google.com/document/d/1BU5C4jFcUKo2r-YCwT0UH-s4Rfb95KvEnHxCzfnMVF8/edit#) for potential fixes to your errors.  If your error is not listed in our guide you may need to look them up in a search engine like Google for possible solutions.
{% endhint %}

#### Creating a Gulp file in our project

We need to create a new file in the root of our project which will contain the code Gulp needs to run the various automated tasks.

1. In your text editor, click **File** &gt; **New File**.  You will see a new empty file
2. Copy the code below and paste it into the new file
3. After pasting the code, click **File &gt; Save**
4. Name the file **gulpfile.js** \(all lowercase and no spaces\)
5. **IMPORTANT:** Be sure you are saving this file in the root of your project.  If when you performed step 1 above you were inside one of your project's directories, by default the system will try to save the new file in that directory.  Be sure you select the top-most directory of your project \(i.e. `components_project`\)
6. Press **Save**

{% tabs %}
{% tab title="gulpfile.js" %}
```javascript
'use strict';

const { series, parallel, watch } = require('gulp');
const { compileSass } = require('./gulp-tasks/compile');
const { lintSass } = require('./gulp-tasks/lint');
const { concatCSS } = require('./gulp-tasks/concat');

exports.compile = parallel(compileSass);

exports.lint = parallel(lintSass);

exports.concat = parallel(concatCSS);

/**
 * @returns {undefined}
 */
function watchFiles() {
  watch(
    './source/_patterns/**/**/*.scss',
    series(parallel(lintSass, compileSass), concatCSS, (done) => {
      done();
    })
  );
}

exports.watch = series(
  parallel(
    lintSass,
    compileSass,
  ),
  parallel(concatCSS),
  series(watchFiles)
);

exports.default = series(
  parallel(
    lintSass,
    compileSass
  ),
  parallel(concatCSS)
);
```
{% endtab %}
{% endtabs %}

* In the interest of space, I have removed all comments from the gulpfile.  If you want to see a commented version check the Resources section in this book.
* While all the tasks we need to run can be included in `gulpfile.js`, I have opted to create separate files for each task.  The code above will look for those individual files to run the tasks. 

#### Add individual Gulp tasks files

We will create 3 new files to complete the workflow setup.  Each of the files is a task we will run with Gulp \(watch, compile, lint\).  Let's create the files now.

1. In the root of your project create a new directory called **gulp-tasks** \(all lowercase\)
2. Inside **gulp-tasks** you will create the following 3 files: **compile.js**, **concat.js**, and **lint.js**
3. Add the code below to each of the files respectively.

{% tabs %}
{% tab title="compile.js" %}
```javascript
'use strict';

// Include gulp
const { src, dest } = require('gulp');

// Include Our Plugins
const sass = require('gulp-sass');
const prefix = require('gulp-autoprefixer');
const rename = require('gulp-rename');

/**
 * Error handler function so we can see when errors happen.
 * @param {object} err error that was thrown
 * @returns {undefined}
 */
function handleError(err) {
  // eslint-disable-next-line no-console
  console.error(err.toString());
  this.emit('end');
}

// Export our tasks.
module.exports = {
  // Compile Sass.
  compileSass: function() {
    return (
      src([
        './source/_patterns/**/**/*.scss',
        '!./source/css/*.scss'
      ])
      .pipe(sass({ outputStyle: 'nested' }).on('error', handleError))
      .pipe(
        prefix({
          cascade: false
        })
      )
      .pipe(
        rename(function(path) {
          path.dirname = '';
          return path;
        })
      )
      .pipe(dest('./public/css'))
    );
  }
};
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="concat.js" %}
```javascript
// Include gulp
const { src, dest } = require('gulp');

// Include Our Plugins.
var concat = require('gulp-concat');
var order = require('gulp-order');

// Export our tasks.
module.exports = {
  // Concat all CSS into a master bundle.
  concatCSS: function () {
    return (
      src([
        './public/css/*.css',
        '!./public/css/all.css',
        '!./public/css/pattern-scaffolding.css'
      ])
        .pipe(order([
          'public/css/style.css',
          'public/css/*.css'
        ], { base: './' }))
        .pipe(concat('all.css'))
        .pipe(dest('./public/css'))
    );
  }
};
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="lint.js" %}
```javascript
'use strict';

// Include gulp
const { src } = require('gulp');

// Include Our Plugins
const gulpStylelint = require('gulp-stylelint');

// Export our tasks.
module.exports = {
  // Lint Sass based on .stylelintrc.yml config.
  lintSass: function () {
    return src([
      './source/_patterns/{00-atoms,01-molecules,02-organisms,03-templates,04-pages}/**/*.scss'
    ])
    .pipe(
      gulpStylelint({
        reporters: [
          {
            formatter: 'string',
            console: true
          }
        ]
      })
    );
  }
};
```
{% endtab %}
{% endtabs %}

* Again, make sure each of the last 3 files above were created inside the **gulp-tasks** directory.  Also ensure their names match the names used above including casing.  If the files do not match you will run into errors and gulp will not work.

#### Updating Pattern Lab so it uses our new workflow

As you may recall, Pattern Lab uses **style.css** to render all of its default CSS styles.  In addition, every time we create a new CSS file, we need to add it to `source/_meta/_00-head.twig` so Pattern Lab can make use of the new CSS styles.  Now that we have a new workflow in place we need to make one final update to `source/_meta/_00-head.twig` so it uses `all.css` file for all CSS including our own custom components.

If you look at the `concat.js` task above, one of the things we've done is we've combined all CSS \(Pattern Lab's and our own custom component's CSS\), into a single stylesheet \(`all.css`\).  By doing this we can tell Pattern Lab to use `all.css` instead of`style.css`.  The beauty of this is that even when we create new CSS files \(or Sass actually since this makes it possible for us to use Sass now\), those files will automatically be compiled into plain CSS and will also be automatically appended to `all.css`.  This means we no longer need to keep adding CSS files to Pattern Lab's `_00-head.twig` 🔥

1. In your text editor open `source/_meta/_00-head.twig`
2. Update the top portion of the file by adding the code below and overriding all other `<link .../>` tags.  Basically the two link tags below should be the only link tags in the page.
3. Save the file

{% tabs %}
{% tab title="\_00-head.twig" %}
```php
<link rel="stylesheet" href="../../css/pattern-scaffolding.css?{{ cacheBuster }}" media="all" />
<link rel="stylesheet" href="../../css/all.css?{{ cacheBuster }}" media="all" />
```
{% endtab %}
{% endtabs %}

* So we're keeping Pattern Lab's `pattern-scaffolding.css` stylesheet untouched.  That's a tiny file so no need to combine it with all the other code
* Then, we added our new `all.css` which contains all the code \(default Pattern Lab code from style.css, and current and future CSS code we write\).
* So from now on, we can create Sass files inside each of the component's directories and Gulp will do the rest for us.

#### Final step:  Adding linting configuration rules

A code linter, whether is CSS or JavaScript, is a great tool to use to ensure the code we write complies with coding standards and best practices.  One of the dependencies we installed above is **Stylelint**, which checks all CSS code we write for compliance.  This is pretty long file so we have made it available as a Github Gist to avoid taking up too much space in this page.  Follow these steps to copy this file's content into your project.

1. [Visit Github's Gist page](https://gist.githubusercontent.com/mariohernandez/be2066f35bc3f66b371ec732fa3e73ab/raw/07ccfafc7e66324d38321e110f13c212be289022/.stylelintrc.yml) to access `.stylelintrc.yml`
2. From the browser's toolbar select **Edit &gt; Select All** 
3. With all content selected, click **Edit &gt; Copy** from the toolbar again
4. In your text editor, create a new file \(File &gt; New \), in the root of **components\_project** and name it `.stylelintrc.yml` \(notice the dot in front of the file name\)
5. Once in the new file, select **Edit &gt; Paste**  from your code editor's toolbar
6. Save the file.

