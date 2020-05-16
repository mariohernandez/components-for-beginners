# Improving Styles

### Color variables

So far we've been using Sass but have not really taken advantage of many of its features.  One extremely power advantage in particular is Variables.  By creating variable we centralized where things get updated in one place, and changes are reflected everywhere where those variables are used.  Let's start by creating color variables.

Pattern Lab comes with a lot of variable already which we could use.  However, they may not necessarily meet our requirements for naming conventions.  Let's take a look at use what we can and create new ones for other things.

1. In your editor open `source/css/scss/generic/_variables.scss`
2. Edit the existing list of color variables so it looks like this:

{% tabs %}
{% tab title="\_variables.scss" %}
```css
//Colors
$navy-blue : #003954;
$gray : #808080;
$gray-light : #edf2f7;
$gray-light-2 : #eee;
$gray-light-3 : #ddd;
$gray-med : #ccc;
$gray-dark : #444;
$gray-dark-2 : #131313;
$white : #fff;
$black : #000;
$dim : rgba(0,0,0,0.5);
$error : #f00;
$valid : #089e00;
$warning : #fff664;
$information : #000db5;
```
{% endtab %}
{% endtabs %}

* We mostly kept the the original names but changed some of the color hex codes to match our own colors.
* Also added the `$navy-blue` variable with our blue.

### Update Pattern Lab's color palette

If you look in Pattern Lab's Atoms &gt; Global, you will see that there is a page for defining a color palette.  This is a great tool for teams to ensure everyone working on the project uses the same colors and things don't get out of hand with multiple variations of the same color.  Since we updated some of our color variables, let's update the color palette page to reflect the new changes.

1. In your editor open `source/_patterns/00-atoms/01-global/00-colors.twig`
2. Replace all the code in the file with the one below

{% tabs %}
{% tab title="00-colors.twig" %}
```php
<ul class="sg-colors">
	<li>
		<span class="sg-swatch" style="background: #003954;"></span>
		<span class="sg-label">#003954</span>
	</li>
	<li>
		<span class="sg-swatch" style="background: #ffffff;"></span>
		<span class="sg-label">#ffffff</span>
	</li>
	<li>
		<span class="sg-swatch" style="background: #edf2f7;"></span>
		<span class="sg-label">#edf2f7</span>
	</li>
	<li>
		<span class="sg-swatch" style="background: #cccccc;"></span>
		<span class="sg-label">#cccccc</span>
	</li>
	<li>
		<span class="sg-swatch" style="background: #808080;"></span>
		<span class="sg-label">#808080</span>
	</li>
	<li>
		<span class="sg-swatch" style="background: #444444;"></span>
		<span class="sg-label">#444444</span>
	</li>
	<li>
		<span class="sg-swatch" style="background: #000000;"></span>
		<span class="sg-label">#000000</span>
	</li>
	<li>
		<span class="sg-swatch" style="background: #ff0000;"></span>
		<span class="sg-label">#ff0000</span>
	</li>
	<li>
		<span class="sg-swatch" style="background: #00ff00;"></span>
		<span class="sg-label">#00ff00</span>
	</li>
	<li>
		<span class="sg-swatch" style="background: #0000ff;"></span>
		<span class="sg-label">#0000ff</span>
	</li>
	<li>
		<span class="sg-swatch" style="background: #ffff00;"></span>
		<span class="sg-label">#ffff00</span>
	</li>
	<li>
		<span class="sg-swatch" style="background: #00ffff;"></span>
		<span class="sg-label">#00ffff</span>
	</li>
	<li>
		<span class="sg-swatch" style="background: #ff00ff;"></span>
		<span class="sg-label">#ff00ff</span>
	</li>
</ul>
```
{% endtab %}
{% endtabs %}

* We added the new colors and also rearranged things a little.
* If you save all the changes you've made and look at Pattern Lab's colors atom, you should see our color palette looking a lot nicer.

### Wait wait, there is more

Adding and updating colors and variables is only half the job.  We still need to update our website so it uses the new variables.

1. In your editor, open `hero.scss` `blog-content.scss`, and `button.scss`
2. At the very first line of each file add the following code:

{% tabs %}
{% tab title="hero.scss & button.scss & blog-content.scss" %}
```css
// Imports variables
@import '../../../css/scss/generic/variables';
```
{% endtab %}
{% endtabs %}

* Since we want to use the new variables, we first need to import them into the files where we want to use them.  This way the variables we want to use are available.  If we don't do this we will get an error that the variable we are trying to use does not exist.
* We need to do this with every SCSS file where we want to use the variables.  Since we know the Hero and Button components as well as the footer use the navy blue color, we need to update both.  If you are using that color in any other SCSS file, add the lines of code above on those files as well.

### Replace any instance of \#003954 with $navy-blue

Currently the Hero, Button and Blog Content components use the navy blue color through its hex code.  We could manually repace the hex code `#003954` with `$navy-blue`.  Or, if you want to make sure you don't miss any instance, you could do a Find and Replace.  Like this:

1. In VS Code, right-click on `_patterns` and select **Find in Folder...** from the dialog box
2. You will see **Search** and **Replace** fields
3. In **Search** type `#003954`
4. In **Replace** type `$navy-blue`
5. Click the tiny little icon to the right of the Search field.  It looks like a little arrow with some letters.
6. You will be shown how many instances of that color there are in your project.  Click **Replace All**
7. Reload Pattern Lab and confirm the navy blue color on buttons Footer, and Hero title still looks correct.  Also check your Gulp task in the command line to ensure there are no errors while compiling the new changes.  If there are errors, you will be told what they are and you should be able to correct them.
8. Repeat these steps with any other colors where we are using hex codes to ensure we are using their variable equivalent.

After all your colors have been updated, if you ever want to change one of the colors, you will only do it in `_variables.scss` and those changes will reflect everywhere in your project where the updated variable is being used. 🔥

### More variables

If you look in `_variables.scss` you will see that there are many more variables for things like typography, spacing, layout, borders, etc.  Those could be handy if you ever need them.  However, there are a set of variables we will for sure use, that's the **Breakpoints**.  These will help us write media queries in Sass to achieve mobile/responsive design in our components and homepage.

Take a look at the [Mobile and beyond](../responsive-design/mobile-and-beyond.md) page to see how we make use of breakpoints.

