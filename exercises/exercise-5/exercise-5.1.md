# Exercise 5.1

### Styling the Homepage

![Homepage](../../.gitbook/assets/components-for-beginners.png)

Although we could create a stylesheet to style the homepage so it matches our designs, it is better to take a step back and think about the requirements for our site. Normally you would not build a one-page website \(although is not unusual for landing pages, brochure-like sites\), but if you are working on a typical project where there will be several landing pages like the one we're building, and especially if those pages will use the components we've built, it is best to look at a global approach to styling those pages.

There are several ways to address the layout and styling of the homepage. One method I've used in the past is creating a Sass mixin to add specific spacing around a component \(typically at the bottom of the component\). If we look at the homepage design comp above we see that the amount of space below each component is the same. Typically for consistency purposes the spacing will remain the same regardless of where the components are used. In the event of a change of that spacing for a given component, we can always plan for a fallback to override the original spacing rules. Let's go with this approach for now.

### Creating a Sass mixin for components spacing

1. In your text editor, open `source/css/scss/generic/_mixins.scss`
2. At the end of the file add the following code:

{% tabs %}
{% tab title="\_mixin.scss" %}
```css
// Mixin for adding consistent spacing on components.
@mixin component-spacing($margin: 100px) {
	margin: 0 auto $margin;
}
```
{% endtab %}
{% endtabs %}

* **@mixin** is a keyword used in Sass to group CSS code that will be reused.  This mixin can used pretty much anywhere in our project.  Our plan is to use in components so we can keep consistent spacing around them.
* **component-spacing** is the name of the mixin.  It is a good idea to name mixins with names that make it easy to determine their function.
* **\($margin: 100px\)** are parameters the mixin accepts.  In this example we are using a variable of `$margin` which will allow us to pass a value.  If no value, is provided when using the mixin we are setting a default of 100px.
* **margin** is the CSS property where we want to add the value of `$margin`\(the bottom margin will use the value of $margin\)

### Using the component-spacing mixin

1. Edit `source/_patterns/01-molecules/hero/hero.scss`
2. Add the new **component-spacing** mixin as the first CSS property to the `.hero` selector.  \(line 5\):

{% tabs %}
{% tab title="hero.scss" %}
```css
@import '../../../css/scss/generic/mixins';
@import '../../../css/scss/generic/variables';

.hero {
  @include component-spacing;
  @include image-crop (300px);
  ...
}
```
{% endtab %}
{% endtabs %}

* In line 1 & 2 we are importing the **mixins** and **variables** Sass partials.  This means any mixins and variables in those partials will be available for us to use in **hero.scss**. 

{% hint style="info" %}
As best practice, mixins should always be added before any other CSS properties as shown above. This makes it possible to override any mixin properties if needed.
{% endhint %}

If your Sass watch task is running you should see the hero now has 100px of space at the bottom. If Sass watch was not running type `gulp watch` and reload Pattern Lab.

### Add the mixin to other Homepage components

Now go ahead and update the other two components used in the homepage, **Featured Content** and **Blog Content**.

* Repeat steps 2 & 3 above
* Ensure the mixin is added the the top most wrapper of each component \(`.featured-content` and `.blog-content`\).  If those selectors don't exist, create them to add the mixin.

### YOU DID IT!! 🏆 🎉 🙌

