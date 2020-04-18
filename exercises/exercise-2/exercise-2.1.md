# Exercise 2.1

### Button component

Buttons are some of those things that used over and over on a website. For this reason it makes sense to create a new atom for the button.

1. Inside `source/_patterns/00-atoms/` create a new directory called **button**
2. Inside the _button_ directory create a new file called **button.json**
3. Inside `heading.json` add the following code:

{% tabs %}
{% tab title="button.json" %}
```yaml
{
  "button": {
    "text": "button",
    "url": "",
    "modifier": ""
  }
}
```
{% endtab %}
{% endtabs %}

We created an object called `button` and added several properties or attributes such as `text`, `url`, and `modifier`.  By now we've seen this kind of data structure on other components.

### Writing the button's logic

1. Inside the _button_ directory create a new file called **button.twig**
2. Inside `button.twig` add the following code:

{% tabs %}
{% tab title="button.twig" %}
```php
{% if button.url %}
  <a href="{{ button.url }}" class="button{{ button.modifier ? ' ' ~ button.modifier }}">
    {{ button.text }}
  </a>
  {% else %}
  <button class="button{{ button.modifier ? ' ' ~ button.modifier }}">
    {{ button.text }}
  </button>
{% endif %}

```
{% endtab %}
{% endtabs %}

* We've added some logic to the button to ensure we render the right HTML element based on the data we receive. For example, if a URL is passed, we use an `<a>` with the class of **button**, otherwise we use a `<button>` tag. We always want to make sure we use proper semantic markup for accessibility and for the task at hand. An `<a>` tag will allow us to be directed to another page or a section within the same page, whereas a `<button>` element will allow us to perform an action such as submit content.

#### Next:  Updated the Hero to make use of the new button atom

