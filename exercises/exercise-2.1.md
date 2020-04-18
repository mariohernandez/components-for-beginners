# Exercise 2.1

### Button component



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

