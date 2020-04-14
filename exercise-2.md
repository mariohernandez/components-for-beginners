# Exercise 2

The next component we will build as part of Exercise 2, is the **Card** component.

![Card component](.gitbook/assets/card.png)

A Card component is a pretty common component on most website because they are perfect for displaying specific type of content.  Typically you will see cards in a group to show things like Latest News, Latest Events, etc.

### Building the Card

One of the first things we need to do is define the data fields that makeup the component.  If you look at the image above, a single Card has the following data fields:

* image
* title \(link to full article\)
* date
* body
* & tags

Now that we have identified the fields our card component needs, let's start building it.

#### Component's stock content

1. Inside _components_ create a new directory called **card**
2. Inside the _card_ directory create a new file called **card.json**
3. Inside _card.json_ add the following code:

{% tabs %}
{% tab title="card.json" %}
```yaml
{
  "image": "<img src='https://placeimg.com/640/350/places' alt='Card image' />",
  "title": {
    "heading_level": "3",
    "title": "The beauty of nature",
    "url": "#"
  },
  "date": "March 16 2020",
  "body_text": "Curabitur blandit tempus porttitor. Vestibulum id ligula porta felis euismod semper. Vivamus sagittis lacus vel augue laoreet rutrum faucibus dolor auctor. Aenean lacinia bibendum nulla sed consectetur.",
  "tags": [
    {
      "text": "Phtography",
      "url": "#"
    },
    {
      "text": "Nature",
      "url": "#"
    },
    {
      "text": "Outdoors",
      "url": "#"
    }
  ],
  "modifier": ""
}
```
{% endtab %}
{% endtabs %}

By now we should be well familiar with the fields structure above.  The one field type we probably have not used much is an array.  In the code above we are declaring the tags as an array.  Each tag item inside the array has a text and URL keys so they can basically become links to tag-driven pages on our site.

#### Component's markup

1. Inside the _card_ directory create a new file called **card.twig**
2. Inside _card.twig_ add the following code:

{% tabs %}
{% tab title="card.twig" %}
```php
{{ attach_library('training_theme/card') }}

<article class="card">
  {%  if image %}
    <div class="card__media">
      {{ image }}
    </div>
  {% endif %}
  {% if title or date or body or tags %}
  <div class="card__content">
    {% if title %}
      {%
        include '@training_theme/heading/heading.twig' with {
          title: title.title,
          heading_level: title.heading_level,
          url: title.url
        } only
      %}
    {% endif %}
    {% if date %}
      <div class="card__date">
        {{ date }}
      </div>
    {% endif %}
    {% if body_text %}
      <p class="card__body">
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
  </div>
  {% endif %}
</article>
```
{% endtab %}
{% endtabs %}

* Most things look pretty straight forward in the code above.  With the tags we loop through the `tags` array and then add each  tag item as a list item in the unordered list.

#### Create the card library.

#### Component styles

1. Inside the _card_ directory create a new file called **card.scss**
2. Inside _card.scss_ add the following code:

{% tabs %}
{% tab title="card.scss" %}
```css
// Import site utilities
@import '../../global/utils/init';

.card {
  display: flex;
  flex-direction: column;
  position: relative;
  max-width: 420px;
  margin: 50px auto 20px;
  border-radius: 4px;
  box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);

  img {
    display: block;
  }

  &.card__wide {

    @include breakpoint($bp-sm) {
      flex-direction: row;

      .card__media,
      .card__content {
        flex: 0 0 50%;
      }
    }
  }
}

.card__content {
  padding: 20px;
}

.card__title {
  margin-bottom: 8px;
  margin-top: 0;
  font-size: 24px;
  font-weight: 600;
}

.eyebrow__text {
  margin: 0;
}

.card__date {
  text-transform: uppercase;
  display: block;
  border-bottom: 1px solid #ccc;
  padding-bottom: 8px;
  letter-spacing: 2px;
}

.card__tags--items {
  display: flex;
  list-style: none;
  margin: 0;
  padding: 0;
}

.card__tag--item {
  background-color: #edf2f7;
  border-radius: 99999px;
  color: #4a5568;
  display: inline-block;
  padding: 4px 10px;
  margin-right: 10px;
}

.card__tag--link {
  text-decoration: none;
  color: #1a202c;

  &:hover,
  &:focus {
    color: lighten(#1a202c, 25%);
  }
}

```
{% endtab %}
{% endtabs %}

#### Compiling the code

Now that the card component is done, let's compile the code so we can see it in Pattern Lab.  If the watch task is running you should be able to see the card component in Pattern Lab, otherwise follow these steps:

While in your theme's root directory, run the following commands in your command line and press **Return**

`npm run build`

`npm run watch`

In your browser of choice open the following URL: [http://localhost:3000](http://localhost:3000). This will open Pattern Lab where you can find the Card component under components.

