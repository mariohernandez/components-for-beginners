# Exercise 3.1

### Building the Card variant

Probably the first thing you should look at to determine if a component is a candidate for variants, is the data fields, and second, the component's markup.

Visually we know the two different variants look similar, however, if we pay close attention we will notice that the data fields between the variants are different. In this particular case although some of the fields may be different, I feel we have enough of shared attributes between the variants that we should have no problem going the variant route vs. new components. Let's start! The new variant will be called **Card wide**.

![Card wide variant](../../.gitbook/assets/card-wide.png)

We can see that the overall layout of the "Card wide" lends itself nicely to a variant. However, we see that some of the fields found in the original card are not present here \(tags\), and, there is also a new field in this variant that is not part of the original card \(button\).

Before we can create a new variant, we need to make some updates to the original Card component so it is easier to adapt it to new variants.

### Modifier class

A CSS modifier class is a pretty common way to make changes to any element. For example, let's say we use two types of buttons in our website; one red and one blue. Using a CSS class like say, `button--blue`, and `button--red` will allow us to change their colors without altering the original button. We will use a similar approach to achieve some of the changes in the Card wide variant.

* Update **card.json** and **card.twig** to be able to pass a value for a modifier class.

{% tabs %}
{% tab title="card.jsoon" %}
```yaml
{
  "modifier": "",
  "image": "...",
  "title": {
  ...
}
```
{% endtab %}
{% endtabs %}

* We updated **card.json** by adding a new key of `modifier` at around line 2 above \(I've excluded most fields to keep the file short and easier to read.  **You should not remove any fields**\).
* This will allow us to pass a value to Twig which we can use as a CSS modifier class.  Before we can make use of this new key, we need to update the Card's  twig template so we can determine where in the card this new value will be added.
* Let's update **card.twig** as follows:

{% tabs %}
{% tab title="card.twig" %}
```php
<article class="card{{ modifier ? ' ' ~ modifier }}">
```
{% endtab %}
{% endtabs %}

The part `{{ modifier ? ' ' ~ modifier }}` is basically a Twig conditional statement asking "Is there a value for modifier in JSON?" if so, print it here along with the class of `card`, but first add an empty space in between the two classes. For example, if the value for modifier in JSON is, `card__wide`, when the card is rendered in Pattern Lab, the `article` wrapper will now look like this:

{% tabs %}
{% tab title="Pattern Lab" %}
```php
<article class="card card__wide">
```
{% endtab %}
{% endtabs %}

Now that we have the modifier key available, you can test it by adding any value to the `modifier` key and running `npm start` to view the card component in Pattern Lab. The Card component should now have, in addition to `card`, the value you added as an extra CSS class.

### CSS updates

In the interest of time, our CSS styles for the card already include styles for when we have a `card__wide` class in addition to `card`. So if you did use **card\_\_wide** as the example value above, you should actually see the card looking different than the original card.

Our test above proves that using a CSS modifier class can help achieve some of the changes in the card variant, however, the goal is to not alter the original Card component when creating the variant. To accomplish this we need to work with Pattern Lab's Pseudo Patterns.

## Pseudo Patterns in Pattern Lab

Pattern Lab uses [Pseudo Patterns ](https://patternlab.io/docs/pattern-pseudo-patterns.html)to create variants of components. Pseudo-patterns are similar to [pattern-specific JSON files](https://patternlab.io/docs/data-pattern-specific.html) but are hinted in such a way that a developer can build a variant of an existing pattern. The basic syntax for pseudo patterns is:

```text
patternName~pseudo-pattern-name.json
```

The tilde \(~\) and .json file extension are the hints that Pattern Lab uses to determine that this is a pseudo-pattern. The **patternName** tells Pattern Lab which existing pattern it should use when rendering the pseudo-pattern. The **pesudooPatternName** tells Pattern Lab the name for the new variant. The JSON file itself works exactly like the [pattern-specific JSON file](https://patternlab.io/docs/data-pattern-specific.html) . It has the added benefit that the pseudo-pattern will also inherit any values from the existing pattern’s pattern-specific JSON file. This is not always a good thing and we will need to address this in our exercise.

From a navigation and naming perspective **patternName** and **pseudoPatternName** will be combined.

### Creating a new variant

* Inside the _card_ directory, create a new JSON file with the following naming convention: `card~wide.json` \(notice the tilde \(~\)  in the file name\). We don't need to create a new Twig file because by default Pattern Lab will use the original card.twig template.  This also will need updating in order for us to achieve our card variant.  More on this later.
* Copy all the code from `card.json` into `card~wide.jsoon`

### Displaying the right fields for the card variant

As indicated above, by default the pseudo pattern file \(`card~wide.json`\), inherits all the fields from `card.json`. This is usually good but in our case, we don't need some of the fields in the Card variant. For example, we don't need the tags or the date fields. In addition, the card title in the variant should not be a link and its text should read "Marie The Producer". And finally, the card variant uses a button but the originally card does not. So how do we manage those fields without affecting the original Card component? Let's take a look:

* Update `card~wide.json` as shown below:

{% tabs %}
{% tab title="card~wide.json" %}
```yaml
{
  "image": "<img src='https://placeimg.com/480/480/places' alt='Card image' />",
  "title": {
    "heading_level": "3",
    "modifier": "",
    "title": "Level up your game",
    "url": ""
  },
  "date": "",
  "category": "Sports",
  "body_text": "Curabitur blandit tempus porttitor. Vestibulum id ligula porta felis euismod semper. Vivamus sagittis lacus vel augue laoreet rutrum faucibus dolor auctor. Aenean lacinia bibendum nulla sed consectetur.",
  "tags": "",
  "cta": {
    "text": "Read the full article",
    "url": "#",
    "modifier": "card__cta"
  },
  "modifier": "card__wide"
}
```
{% endtab %}
{% endtabs %}

* Let's start with the new fields.  As you can see we have added the **job\_title** and **cta** fields.  If you are wondering why not use the date field for the job\_title since they look exactly the same, technically a date and text string fields wold typically be different field types on most content management systems like Drupal.  That's why we are using different fields here.
* Next, for those fields we don't need, we are declaring them with no values.  If we simply remove them, they would be inherited from `card.json` and by leaving their values empty, they will not be rendered on a page because when we built the `card.twig` template we wrapped each field in an `if` statement.  This basically means that if a field does not exist or has no values, it will never be printed on the page.  Slick huh?

### Updating card.twig

Our variant JSON is ready with only the fields we want. However, we still need to update card.twig as it currently does not use a button field. There are several ways to add the button to only the variant. We'll take a look at the two easiest ways:

### Twig conditional statements

The same way we did the the other fields, we can wrap the button field in a twig `if` statement so it would only print if the field exists or has values in the .JSON file. Since the original .JSON file does not have a button or **cta** field, the button will not be available in the original card component. And since we did add a button to `card~wide.json`, then the button will be available in the card wide variant. Let's take a look at how this will look in twig.

{% tabs %}
{% tab title="card.twig" %}
```php
<article class="card{{ modifier ? ' ' ~ modifier }}">
  {%  if image %}
    <div class="card__media">
      {{ image }}
    </div>
  {% endif %}
  {% if title or date or job_title or body or tags or cta %}
  <div class="card__content">
    {% if title %}
      {%
        include '@atoms/heading/heading.twig' with {
          heading: title
        } only
      %}
    {% endif %}
    {% if date %}
      {%
        include '@atoms/eyebrow/eyebrow.twig' with {
          eyebrow: {
            text: date,
            modifier: 'card__date'
          }
        } only
      %}
    {% endif %}
    {% if job_title %}
      {%
        include '@atoms/eyebrow/eyebrow.twig' with {
          eyebrow: {
            text: job_title,
            modifier: 'card__eyebrow'
          }
        } only
      %}
    {% endif %}
    {% if body_text %}
      <p class="card__body-text">
        {{ body_text }}
      </p>
    {% endif %}
    {% if tags %}
      <ul class="card__tags--items">
        {% for item in tags %}
          <li class="card__tag--item">
            <a href="{{ item.url }}" class="card__tag--link">
              {{ item.text }}
            </a>
          </li>
        {% endfor %}
      </ul>
    {% endif %}
    {% if cta %}
      {%
        include '@atoms/button/button.twig' with {
          button: cta
        } only
      %}
    {% endif %}
  </div>
  {% endif %}
</article>
```
{% endtab %}
{% endtabs %}

* On line 7, we updated the `if` statement to include job\_title and cta.  This may seem extreme but using conditional statements is a good practice to ensure you are not printing or rendering HTML elements, like a `<div>`, when there is no content inside of it.
* In line 28, we are adding the `job_title` field, also inside an `if` statement.
* Finally in line 52, we added the `cta` field to show the button.
* Now if we save our changes, we should see the two card variants in Pattern Lab, one with tags and a date field, and the other one without tags or date fields, but with a button.  In addition, the Card wide variant's layout is horizontal vs. the original card has a vertical layout.

If you don't have Pattern Lab running, run this command: `npm start`.

