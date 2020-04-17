# Exercise 1.1

### Improving the Heading component

The heading component looks good and it will work great, ...as long as we always want to use a `<h1>`. However, the component is pretty static and it does not offer much flexibility. What if we wanted to use a h2 or h3? or what if the title field is a link to another page? Then the heading component would probably not work because we have no way of changing the heading level from h1 to any other level or add a URL. Let's re-work the heading component so we make it more dynamic.

### Update Heading's data structure

* Inside `source/_patterns/00-atoms/heading/` create a new file called **heading.json**
* Inside `heading.json` add the following code: \(mind indentation\)

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

By creating a `heading.json` file in the same directory as `heading.twig`, we are opting to create our own data file for the heading component and by doing so we can change what properties the heading component can contain.

* **heading\_level** will allow us to change the headings from say, h1 to h2 if we need to
* **modifier** will allow us to add custom CSS classes to titles which will be useful to style some titles different than others
* **title** is the key for the title text when using the heading component
* ... and **url**, if present, will allow us to wrap the title in an `<a>` tag, to make it a link.

**NOTE:**  The order of the properties above has no effect on how components work or get rendered in Pattern Lab.  I have opted to organize each property alphabetically.

### Update the heading's markup and logic

* Update the `heading.twig` file to look like this:

{% tabs %}
{% tab title="heading.twig" %}
```php
<h{{ heading_level|default('2') }} class="heading{{ modifier ? ' ' ~ modifier }}">
  {% if url %}
    <a href="{{ url }}" class="heading__link">
      {{ title }}
    </a>
  {% else %}
    {{ title }}
  {% endif %}
</h{{ heading_level|default('2') }}>
```
{% endtab %}
{% endtabs %}

Wow! What's all this? 😮

Let's break things down to explain what's happening here since the twig code has changed significantly:

* Line 1, makes use of `heading_level` to complete the number part of the heading.  If a value is not provided for `heading_level` in the JSON file, we are setting a default of `2`.  This will ensue that by default we will have a `<h2>` as the title, much better than `<h1>` as we had before.  This value can be changed per use case if needed.  Line 9 closes the heading tag the same way.
* Also in line 1, we have added a placeholder for `modifier` so if we choose to add a value it will be added as a CSS class along with `heading`.  More on this later.
* In line 2, we check whether a URL was provided in the JSON file, and if so, we wrap the `{{ title }}` variable in an `<a>` tag to turn the title into a link.  The **href** value for the link is `{{ url }}`.  If no URL is provided in the JSON file, we simply print the value of `{{ title }}`as plain text.

### Compiling the code

After saving the changes above Pattern Lab should had autoo reloaded.  If this is not the case you can run:

```text
npm start
```

**Just for fun 💥**

* Try changing the heading level in `heading.json` to anything other than H2.
* If you look in Pattern Lab you should see your heading component use the new heading level.

**Congratulations!** You just built your first reusable component! 🙌 🎉

