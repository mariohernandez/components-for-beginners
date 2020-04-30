# Exercise 2.5

### Taking our new Gulp workflow for a test drive

So our gulp workflow is in place, but how do we know it works?  How about if we update the CSS files we created for the Button, Hearing and Hero components?  Great idea! 💡

1. Move `button.css`, `heading.css`, and `hero.css` from `source/css` into each of the respective components.  If you are using VS Code you can literally drag the files into each of the components.
2. Rename each CSS file in the components as `button.scss`, `heading.scss`, and `hero.scss`

Sass is a CSS Preprocessor and it provides all kinds of advantages over plain CSS.  The most commonly used Sass syntax is known as “**SCSS**” \(for “Sassy **CSS**”\), and is a superset of CSS3's syntax.  SCSS syntax is easy to learn as it most closely resembles CSS syntax.  In fact, if you noticed in step 2 above, all we did to start using .SCSS was to rename files from `.css` to `.scss` and that's it, we are now using Sass. 🤯

### Running Gulp

Alright, let's run gulp for the first time and let's cross our fingers that everything works 🤞

1. While in **components\_project** in your command line tool, run `gulp`



