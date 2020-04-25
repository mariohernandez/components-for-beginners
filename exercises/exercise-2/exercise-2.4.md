# Exercise 2.3

## Implement Sass workflow
Pattern Lab out of the box provides provides a basic workflow for writing CSS for components. Unfortunately this is not an optimal way to manage CSS assets in a project.  It requires manual intervention every time a new CSS file is created for a component.  We are going to implement a simple automated workflow to achieve two goals:

1. Write a component's CSS/Sass within the component's directory.  This way each component will contain styles only intended for the component
2. Combine all compiled CSS into a single stylesheet to automate Pattern Lab's styling of co
mponents in the browser. This will solve Pattern Lab's process to manually add each new stylesheet by hand

Our new workflow will need the following:

* Add Gulp and its dependencies to our project.  Gulp is a task runner which will allow us to perform certain tasks such as compile Sass code into CSS.
* Change location of source CSS code to `_patterns`
* Ensure our CSS code complies with standards and best practices by using a code linter

This will be as basic of a workflow as it gets but will make it possible to us to use Sass instead of plain CSS.  Let's start.

### Add Gulp and other node dependencies

1. In your code editor open `package.json`, which is located in the root of your project
2. Scroll to the bottom of the file until you get to the `dependencies` section (at around line 21)
3. Add the following code directly after the last item (`"@pattern-lab/uikit-workshop": "^5.7.2"`).

    {% hint style="warning" %}
    Add a comma on the last item under dependencies before adding the code below.  In addition, ensure the indentation of the new dependencies below match the rest of the file's indentation.
    {% endhint %}

    {% tabs %}
    {% tab title="package.json" %}
    ```json
    "browser-sync": "^2.26.7",
    "gulp": "^4.0.2",
    "gulp-autoprefixer": "^7.0.1",
    "gulp-changed": "^4.0.2",
    "gulp-concat": "^2.6.1",
    "gulp-eslint": "^6.0.0",
    "gulp-order": "^1.2.0",
    "gulp-rename": "^1.4.0",
    "gulp-sass": "^4.0.2",
    "gulp-stylelint": "^11.0.0",
    "stylelint": "^12.0.1",
    "stylelint-scss": "^3.13.0"
    ```
    {% endtab %}
    {% endtabs %}

4. Save your changes.
