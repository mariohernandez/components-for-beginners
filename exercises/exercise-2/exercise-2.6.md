# Exercise 2.6

### Improving our CSS

So now that we have functioning Sass in our project, let's take a moving to improve the CSS we've written thus far so that we take advantage of some of the features of Sass.

#### Updated the existing CSS

Update `.button.scss`, `.heading.scss`, and `.hero.scss` as follows:

{% tabs %}
{% tab title="button.scss" %}
```css
@import '../../../css/scss/generic/variables';

.button {
  background-color: #003954;
  border: 2px solid #003954;
  color: #ffffff;
  display: inline-block;
  font-size: 16px;
  line-height: 1.3;
  padding: 15px 40px;
  text-transform: uppercase;
  text-decoration: none;

  // Hover and focus states for base button
  &:hover,
  &:focus {
    color: #ffffff;
  }

  // Styles for white button with gray outline.
  &.button--ghost {
    background-color: transparent;
    border: 2px solid #444444;
    color: #444444;
    padding: 8px 30px;

    // Hover and focus styles for ghost button.
    &:hover,
    &:focus {
      color: #444444;
    }
  }
}
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="heading.scss" %}
```css
@import '../../../css/scss/generic/variables';

.heading {
  color: #ff9900;

  // Removes underline when headings are links.
  a {
    text-decoration: none;
  }

  // Styles for extra large headings.
  &.heading--large {
    color: #444444;
    font-size: 100px;
  }
}
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="hero.scss" %}
```css
@import '../../../css/scss/generic/mixins';
@import '../../../css/scss/generic/variables';

.hero {
  @include component-spacing;
  position: relative;

  // Styles heading when inside the hero.
  .heading {
    color: #003954;
    font-weight: 900;
    margin-bottom: 50px;
    text-transform: uppercase;
  }

  img {
    display: block;
  }
}

.hero__content {
  position: absolute;
  text-align: center;
  top: 45%;
  width: 100%;
}
```
{% endtab %}
{% endtabs %}

