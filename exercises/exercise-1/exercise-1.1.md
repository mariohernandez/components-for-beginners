# Exercise 1.1

### Improving the Heading component

The heading component looks good and it will work great ...as long as we always want to use a `<h1>`for all titles. Since our goal for creating any component is to make them reuseable, the current state of the Heading component does not offer much flexibility. What if we wanted to use a h2 or h3? or what if the title field is a link to another page? Then the heading component would probably not work because we have no way of changing the heading level from h1 to any other level or add a URL. Let's re-work the heading component to make it more dynamic.

#### Create a data file for the Heading's

We will start by creating our own data file for this and future components. We will resume using global data from data.json when we build the content lists and homepage prototype at the end of this training.  Follow these steps:

1. Inside `source/_patterns/00-atoms/heading/` create a new file called **heading.json**
2. Inside `heading.json` add the following code: \(mind indentation\)

{% tabs %}
{% tab title="heading.json" %}
```bash
{
  "heading_level": "",
  "modifier": "",
  "title": "This is my website's title",
  "url": ""
}
```
{% endtab %}
{% endtabs %}

By creating a `heading.json` file in the same directory as `heading.twig`, Pattern Lab will use its data vs. the data in data.json.  It is important that the JSON and Twig file names match.  This is the approach we will take for most component going forward.

* **heading\_level** will allow us to change the headings from say, h1 to h2 if we need to
* **modifier** will allow us to add custom CSS classes to titles which will be useful to style some titles different than others
* **title** is the text that will be printed on a page as a page or component title
* ... and **url**, if present, will allow us to turn the title into a link

**NOTE:**  The order of the properties above has no effect on how components work or get rendered in Pattern Lab.  I have opted to organize each property alphabetically.  Sometimes it also makes sense to organize the keys in the order they visually appear on the component.

#### Update the heading's markup and logic

Since we created a new data file for Heading and we have added more keys, we need to update `heading.twig` so it can make use of everything we just did in heading.json.

* Update the `heading.twig` file to look like this: 

{% tabs %}
{% tab title="heading.twig" %}
```php
<h{{ heading_level|default(2) }} class="heading{{ modifier ? ' ' ~ modifier }}">
  {% if url %}
    <a href="{{ url }}">{{ title }}</a>
  {% else %}
    {{ title }}
  {% endif %}
</h{{ heading_level|default(2) }}>
```
{% endtab %}
{% endtabs %}

Wow! What's all this? 😮

Let's break things down to explain what's happening here since the twig code has changed significantly:

* Line 1, makes use of `heading_level` to complete the number part of the heading tag \(i.e. `<h3>`\).  If a value is not provided for `heading_level` in the JSON file, we are setting a default of `2`.  This will ensue that by default we will have a `<h2>`.  This value can be changed per use case if needed.  Line 7 closes the heading tag the same way. By not providing a default/backup value we could potentially end up with a broken heading tag if a value is not passed somewhere.
* Also in line 1, we have added a placeholder for `modifier` so if we choose to pass a value it will be added as a CSS class along with `heading`.  More on this later.
* In line 2, we check whether a URL was provided in the JSON file, and if so, we wrap the `{{ title }}` variable in an `<a>` tag to turn the title into a link.  The `href` value for the link is `{{ url }}`.  If no URL is provided in the JSON file, we simply print the value of `{{ title }}`as plain text.

### CSS Styles

Let's create a CSS file to write basic CSS styles for the heading.

1. Inside the `source/css` folder create a new file called  **heading.css**
2. Inside `heading.css` add the following code:

{% tabs %}
{% tab title="heading.css" %}
```css
.heading {
  color: #ff9900;
}

.heading a {
  text-decoration: none;
}

.heading.heading--large {
  font-size: 125px;
  text-transform: uppercase;
}
```
{% endtab %}
{% endtabs %}

* These are just temporary styles.  We will come back to them later on.

### Oh no! It didn't work 🙀

Out of the box Pattern Lab does not have a an automated system to become aware of new CSS stylesheets that are created. This is a manual process which is not complicated at all. However, on a typical project this should be an automated process. We will implement a basic system to automate this process later on. For now follow these steps to make Pattern Lab aware of`heading.css` .

#### Add the new CSS file to Pattern Lab

1. In your text editor, open `source/_meta/_00-head.twig`
2. Add the following line at the top of the file \(around line 10, directly after other similar lines\), and Save the file.

{% tabs %}
{% tab title="\_00-head.twig" %}
```markup
<link rel="stylesheet" href="../../css/heading.css?{{ cacheBuster }}" media="all" />
```
{% endtab %}
{% endtabs %}

_We added a link to the new CSS file we created for the Heading component.  This will ensure any styles we write for the heading will be available in Pattern Lab._

#### Compiling the code

After saving the changes above Pattern Lab should had auto reloaded.  If not, run this command and press **Return**:`npm start`

**Just for fun 💥**

* Try changing the heading level in `heading.json` to anything other than 2.
* If you look in Pattern Lab you should see your heading component use the new heading level.
* Try adding a value for URL \(i.e. http://google.com\), and the title will become a link.

**Congratulations!** You just built your first reusable component! 🙌 🎉

