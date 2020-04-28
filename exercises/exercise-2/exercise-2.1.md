# Exercise 2.1

## Button component

Buttons are some of those things that are used over and over on a website. For this reason it makes sense to create a new atom for the button.

1. Inside `source/_patterns/00-atoms/` create a new directory called **button**
2. Inside the _button_ directory create a new file called **button.json**
3. Inside `button.json` add the following code:

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

We created an object called `button` and added several properties or attributes such as `text`, `url`, and `modifier`. By now we've seen this kind of data structure on other components.

If you are wondering why we are nesting all the button properties inside a **button** object instead of writing everything on its own as we did with **heading.json** in the previous exercise.  This sometimes is a personal preference or it could also be a hard data requirement.  I personally like to use objects as we've done above as this helps in two ways:

1. It simplifies the component nesting process by not having to map or associate each individual property when we use includes.  You'll see what I mean shortly,
2. If we are creating components or pages where we are reusing several other components, we may run into the issue of components using the same property names.  If this is the case we would need to change property names as JSON will not allow us to use the same key name more than once.  Using objects to nest the properties solves this issue.  

## Writing the button's logic

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

* We've added some logic to the button to ensure we render the right HTML element based on the data we receive. For example, if a URL is passed, we use an `<a>` tag with the class of **button**, otherwise we use a `<button>` tag. We always want to make sure we use proper semantic markup for accessibility and for the task at hand. An `<a>` tag will allow us to link to another page or a section within the same page, whereas a `<button>` element will allow us to perform an action such as submit content.

### Next:  Update the Hero to make use of the new button atom

