# Exercise 2.3

## Update the Heading component by making it an object

So if objects work so great, why don't we do the same for the Heading?  Sure!  Let's do that now.

1. Open `heading.json` in your text editor
2. Update its code so it looks like this:

{% tabs %}
{% tab title="heading.json" %}
```yaml
{
  "heading": {
    "heading_level": "",
    "modifier": "",
    "title": "This is my website's title",
    "url": ""
  }
}
```
{% endtab %}
{% endtabs %}

* We are u sing the same JSON keys as before except now we are nesting them into the `heading` object.

1. In your text editor open `heading.twig`
2. Update the file's code to look like this:

{% tabs %}
{% tab title="heading.twig" %}
```php
<h{{ heading.heading_level|default(2) }} class="heading{{ heading.modifier ? ' ' ~ heading.modifier }}">
  {% if heading.url %}
    <a href="{{ heading.url }}">{{ heading.title }}</a>
  {% else %}
    {{ heading.title }}
  {% endif %}
</h{{ heading.heading_level|default(2) }}>
```
{% endtab %}
{% endtabs %}

* Pretty much the only thing we are doing is appending `heading.` before each of the properties in the code.  Since each property is now nested in the `heading` object, instead of writing `{{ heading_level }}` we need to write `{{ heading.heading_level }}`.  And we are doing the same for each property.

### Update the Hero component

Now that the data structure for Heading has changed, the code we have in the Hero will not work.  So let's update the Hero so it matches the data structure from heading.json.

Notice that in `hero.json` we are already using an object for the **heading** field.  So we don't need to do anything there.

1. In your text editor open `hero.twig`
2. Update the code so the `heading` include looks like this:

{% tabs %}
{% tab title="hero.twig" %}
```php
{% if heading %}
  {%
    include '@atoms/heading/heading.twig' with {
      "heading": heading
    } only
  %}
{% endif %}
```
{% endtab %}
{% endtabs %}

* That's so much better.  Since both **heading** objects in `heading.json` and `hero.json` use the same properties, all we need to do is associate the top objects.  
* **VERY IMPORTANT**:  The object names don't need to match for this to work.  However, their properties do.  If you recall, in the **Button** exercise, the objects did not match \(button & cta\), but because their properties matched, we were still able to just associate the object's names in `hero.twig` \(i.e. `"button": cta`\).

