# Exercise 3.2 \(Optional\)

### Eyebrow component

Did you notice the following code in the card.twig?

{% tabs %}
{% tab title="card.twig" %}
```php
{% if date %}
  <div class="card__eyebrow">{{ date }}</div>
{% endif %}
{% if category %}
  <div class="card__eyebrow">{{ category }}</div>
{% endif %}
```
{% endtab %}
{% endtabs %}

Although Date and Category are two different field types \(date & text\), they both look similarly when rendered in either card variant.  So why not create a new pattern we can use for such type of elements on our site?  So glad you asked 🙌

Creating a new pattern for these kind of elements will make it easier to handle styles and behavior of such elements. 

### Building the Eyebrow component

1. Using either the **Button** of **Heading** components as examples, create a new component called **Eyebrow**
2. The new component's object name in JSON should be `eyebrow`, and its properties or keys should be `text` and `modifier` 
3. Update `card.twig` so you use the new **Eyebrow** component for the Date and Category fields using twig `@include` statements
4. Use the styles below to style the Eyebrow using its own stylesheet \(`eyebrow.scss`\)

{% tabs %}
{% tab title="eyebrow.scss" %}
```css
@import '../../../css/scss/generic/mixins';

.eyebrow {
  text-transform: uppercase;
}
```
{% endtab %}
{% endtabs %}

