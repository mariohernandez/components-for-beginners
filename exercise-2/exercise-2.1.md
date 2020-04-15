# Exercise 2.1

Probably the first thing you should look at to determine if a component is a candidate for variants, is the data fields, and second, the component's markup.

Visually we know the two different variants look similar, however, if we pay close attention we will notice that the data fields between the variants are different. In this particular case although some of the fields may be different, I feel we have enough of shared attributes between the variants that we should have no problem going the variant route vs. new components. Let's start! The new variant will be called **Card wide**.

![Card wide variant](../.gitbook/assets/card-wide.png)

We can see that the overall layout of the "Card wide" lends itself nicely to a variant. However, we see that some of the fields found in the original card are not present here \(tags\), and, there is also a new field in this variant that is not part of the original card \(button\).

Before we can create a new variant, we need to make some updates to the original Card component so it is easier to adapt it to new variant.

#### Modifier class

A CSS modifier class is a pretty common way to make  changes to any element.  For example, let's say we use two types of buttons in our website; one red and one blue.  Using a CSS class of say, `button--blue`, and `button--red` will allow us to change their colors without altering the original button.  We will use a similar approach to achieve some of the changes in the Card wide variant.  First we need to update **card.json** and **card.twig** to be able to pass a value for a modifier class.

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

We updated **card.json** by addint a new key of `modifier` at around line 2 above \(i've excluded most fields to keep the file short and easier to read.  **You should not remove any fields**\).  This will allow us to pass a value to Twig which we can use as a css modifier class.  Before we can make use of this new key, we need to update the Card's  twig template so we can determine where in the card this new value will be added.  Let's update **card.twig** as follows:

{% tabs %}
{% tab title="card.twig" %}
```php
<article class="card{{ modifier ? ' ' ~ modifier }}">
```
{% endtab %}
{% endtabs %}

The part `{{ modifier ? ' ' ~ modifier }}` is basically a Twig conditional statement asking "Is there a value for modifier in JSON? if so, print it here along with the class of `card`, but first add an empty space in between the two classes. For example, if the value for modifier in JSON is, `card__wide`, when the card is rendered in Pattern  Lab, the `article` wrapper will now look like this:

```php
<article class="card card__wide">
```

Now  that  we have the modifier key available, you can test it by adding any value to the `modifier` key and running `npm start` to view the card component in Pattern Lab.  The Card component should now have, in addition to `card`, the value you added as a CSS class.

#### CSS updates

In the interest of time, our CSS styles for the card already include styles for when we have a `card__wide` class in addition to `card`.  So if you did use **card\_\_wide** as the example value above, you should actually see the card looking different than the original card.

Our test above proves that using a CSS modifier class can help achieve some of the changes in the card variant, however, the goal is to not alter the original Card component when creating the variant.  To accomplish this we need to work with Pattern Lab's Pseudo Patterns.

### Pseudo Patterns in Pattern Lab

Pattern Lab uses [Pseudo Patterns ](https://patternlab.io/docs/pattern-pseudo-patterns.html)to create variants of components. Pseudo-patterns are similar to [pattern-specific JSON files](https://patternlab.io/docs/data-pattern-specific.html) but are hinted in such a way that a developer can build a variant of an existing pattern. The basic syntax:

This is the current structure of the Card component

```text
|--card
|  |-- card.twig
|  |-- card.json
```

### Creating a new variant

* Inside the _card_ directory, create a new JSON file with the following naming convention: `card~wide.json` \(notice the tilde \(~\)  in the file name\).  The tilde \(`~`\) and `.json` file extension are the hints that Pattern Lab uses to determine that this is a pseudo-pattern. The `card` part of the file name, tells Pattern Lab which existing pattern it should use when rendering the pseudo-pattern. The JSON file itself works exactly like the [pattern-specific JSON file](https://patternlab.io/docs/data-pattern-specific.html). It has the added benefit that the pseudo-pattern will also inherit any values from the existing pattern’s pattern-specific JSON file. This is not always a good thing and we will need to address this in our exercise.
* The structure of the card component should now look like below.  We don't need to create a new Twig file because by default Pattern Lab will use the original card.twig template.  This also will need updating in order for us to achieve our card variant.

```text
|--card
|  |-- card.twig
|  |-- card.json
|  |-- card~wide.json
```

