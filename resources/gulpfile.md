# Gulpfile

Fully commented gulpfile.js file.

{% tabs %}
{% tab title="gulpfile.js" %}
```javascript
'use strict';

// Include gulp helpers.
const { series, parallel, watch } = require('gulp');

// Include Our tasks.
//
// Each task is broken apart to it's own node module.
// Check out the ./gulp-tasks directory for more.
const { compileSass } = require('./gulp-tasks/compile');
const { lintSass } = require('./gulp-tasks/lint');
const { concatCSS } = require('./gulp-tasks/concat');

// Compile Sass
exports.compile = parallel(compileSass);

// Lint Sass
exports.lint = parallel(lintSass);

// Concat all CSS
exports.concat = parallel(concatCSS);

/**
 * Watch Sass changes
 * @returns {undefined}
 */
function watchFiles() {
  // Watch all sass files and compile sass if a file changes.
  watch(
    './source/_patterns/**/**/*.scss',
    series(parallel(lintSass, compileSass), concatCSS, (done) => {
      done();
    })
  );
}

// Watch task that runs a browsersync server.
exports.watch = series(
  parallel(
    lintSass,
    compileSass,
  ),
  parallel(concatCSS),
  series(watchFiles)
);

// Default Task
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

