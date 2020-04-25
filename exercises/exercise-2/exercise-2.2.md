# Exercise 2.2

### Update Hero

Now that we have a reusable button pattern let's put it to use in the Hero component.  This will help us address any button-releated task from a single component vs. hard-coded links.

* Update the `cta` object in `hero.json` by adding a modifier class as follows:

{% tabs %}
{% tab title="hero.json" %}
```yaml
"cta": {
  "text": "Get started",
  "url": "#",
  "modifier": "hero__cta"
},
```
{% endtab %}
{% endtabs %}

* Inside `hero.twig` change the top portion code to look like the bottom portion of code:

{% tabs %}
{% tab title="hero.twig" %}
```php
// Change this code:
<a href="{{ cta.url }}" class="button hero__cta">
  {{ cta.text }}
</a>

// to this:
{%
  include '@atoms/button/button.twig' with {
    button: cta
  } only
%}
```
{% endtab %}
{% endtabs %}

* In `hero.twig` we are now using a Twig include to use the new button component.  Notice that because we created objects for button and cta, we only need to match the top level object.  Since all properties inside both objects are identical, this property matching happens automatically.

After saving your changes and Pattern Lab reloads, you should not see any difference except now the Hero component is using a button atom.
