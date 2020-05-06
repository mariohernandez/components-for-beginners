# Exercise 5

## Homepage prototype

It is now time to put all the pieces together to build the homepage shown above. Building prototype pages in Pattern Lab is a great way to demo to stakeholders and team members the end product of a project. This is particularly useful for testing.

Building the page will be relatively easy because all we need to do is include all the components we already built. Since we already created sample data in `data.json` for the Featured Content and Blog Content sections in the previous two exercises, we can reuse it for the homepage. We just need to add data for the Hero component in `data.json`. Let's do that now.

### Demo content

1. In your text editor open `source/_data/data.json`
2. Scroll to the end of the file and before the last curly bracket \( } \), add a comma and press **Return**
3. Copy the code below and paste it in the empty space you just created in the previous step.  Ensure the indentation of the newly added code matches the current indentation in the file. 

{% tabs %}
{% tab title="data.json" %}
```yaml
"hero_new": {
  "image": "<img src='https://source.unsplash.com/M6XC789HLe8/1900x700' alt='Yosemite' />",
  "heading": {
    "heading_level": "1",
    "modifier": "hero__title heading--large",
    "title": "Leveling Up",
    "url": ""
  },
  "cta": {
    "text": "Get started",
    "url": "#",
    "modifier": "hero__cta"
  }
}
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
**WARNING**: Ensure you are using/matching the file's indentation preferences for code \(i.e. 2 spaces\). In addition, as we saw in the [JSON Basics](../../basics/json-basics.md) section, ensure you adhere to JSON's punctuation rules \(i.e. commas between each data objects except on the last item.
{% endhint %}

* As you can see above, we are creating an object for the Hero component called **hero\_new**.  Why hero\_new? you may ask yourself.  If you look in `data.json` you will find that there is a `hero:` key.  Rather than overriding the existing key and risking breaking patterns that may already be using it, we're starting with a new object.
* The data structure above was copied from the Hero component we built.

### Building the Twig template for homepage

Now that we have all the data we need, let's build the Twig template that will become our new homepage. As we did with the components we built, we will be using our own naming convention by excluding the numeric prefixes found in patterns provided by Pattern Lab. This is only a personal preference and you are welcome to use Pattern Lab's naming convention if that suits you better.

### Create the Homepage page

1. Inside `source/_patterns/04-pages/` create a new file called **homepage.twig**
2. In _homepage.twig_ write the following code to add the Hero component to the page:

{% tabs %}
{% tab title="homepage.twig" %}
```php
{%
  include '@molecules/hero/hero.twig' with {
    "image": hero_new.image,
    "heading": hero_new.heading,
    "cta": hero_new.cta
  } only
%}
```
{% endtab %}
{% endtabs %}

* Notice how we are only including the **hero** component and mapping its fields to the fields/keys in `data.json`.  We are not writing any HTML.  

If you save your changes and you have Pattern Lab running you should see Homepage in Pattern Lab's "Pages" dropdown \(it should be at the bottom of the list\).  Clicking Homepage should display a new page with a hero in it.

If Pattern Lab was not running run `npm start` to start it.

### Adding the Featured Content List component

When we built the Featured Content List component we added its data to `data.json`. This means we don't have to do anything for data for the homepage.  We can use the same data we already created. All we have to do now is include that component in `homepage.twig` and map its fields accordingly.

1. In _homepage.twig_ write the following code and save your changes:
2. For readability, you may want to leave an empty line in between each component's include.

{% tabs %}
{% tab title="homepage.twig" %}
```php
{% include '@organisms/featured-content/featured-content.twig' %}
```
{% endtab %}
{% endtabs %}

This include statement above is much different and simpler. Since the data for Featured Content List was originally created in `data.json`, Pattern Lab is smart enough to automatically retrieve all the keys and values. This eliminates the need to map each field as we did with the Hero.

Pattern Lab should now show in addition to Hero, the Featured Content list. Don't worry about the spacing around the components for now. We'll address that shortly.

### Adding the Our Blog List component

Go ahead and add the last component on your own. This will be similar to the Featured Content List above.

### Adding the Footer component

We'll keep the footer simple.  Just add Pattern Lab's default footer shown below:

{% tabs %}
{% tab title="homepage.twig" %}
```php
{% include "@organisms/00-global/01-footer.twig" %}
```
{% endtab %}
{% endtabs %}

