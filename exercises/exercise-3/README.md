# Exercise 3

## Card

The next component we will build as part of Exercise 2, is the **Card** component.

![Card component](../../.gitbook/assets/card.png)

A Card component is a pretty common component on most website because they are perfect for displaying specific type of content. Typically you will see cards in a group to show things like Latest News, Latest Events, etc.

### Building the Card

One of the first things we need to do is define the data fields that makeup the component. If you look at the image above, a single Card has the following data fields:

* image
* title \(link to full article\)
* date
* body
* & tags

Now that we have identified the fields our card component needs, let's start building it.

#### Component's stock content

1. Inside _source/\_patterns/01-molecules_ create a new directory called **card**
2. Inside the _card_ directory create a new file called **card.json**
3. Inside `card.json` add the following code:

{% tabs %}
{% tab title="card.json" %}
```yaml
{
  "image": "<img src='https://source.unsplash.com/BJrgqUKYx8M/640x360' alt='Women running' />",
  "title": {
    "heading_level": "2",
    "modifier": "card__title",
    "title": "Level up your game",
    "url": "#"
  },
  "date": "March 16 2020",
  "body_text": "Curabitur blandit tempus porttitor. Vestibulum id ligula porta felis euismod semper. Vivamus sagittis lacus vel augue laoreet rutrum faucibus dolor auctor. Aenean lacinia bibendum nulla sed consectetur.",
  "tags": [
    {
      "text": "Photography",
      "url": "#"
    },
    {
      "text": "Sports",
      "url": "#"
    },
    {
      "text": "Outdoors",
      "url": "#"
    }
  ]
}
```
{% endtab %}
{% endtabs %}

Most fields above are pretty straight forward. For the title we created an object so we can group all title-related properties together. For tags, we are using an array. An array is a list of items all with the same or similar properties. Each tag item inside the array has a text and URL keys.

#### Component's markup

1. Inside the _card_ directory create a new file called **card.twig**
2. Inside `card.twig` add the following code:

{% tabs %}
{% tab title="card.twig" %}
```php
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
        include '@atoms/heading/heading.twig' with {
          heading: title
        } only
      %}
    {% endif %}
    {% if date %}
      <div class="card__eyebrow">{{ date }}</div>
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
  </div>
  {% endif %}
</article>
```
{% endtab %}
{% endtabs %}

* Just like we did with previous components, we are first checking if there is content to render before declaring the fields and their wrappers
* We are re-using the **heading** component by using an `@include` statatement and mapping each key to the respective key from the card's JSON.  We may need to update this later to streamline the nesting process.
* With the tags we loop through the `tags` array and then add each tag item as a list item in the unordered list.  Using `<ul>...</ul>` for listing of content like this is best practice
* Just as we did with the Hero and other components, we are using BEM to name the CSS classes.  We are also setting a namespace for this coomponent by naming each class with `card__*`

#### Component styles

1. Inside the _css_ directory create a new file called **card.css**
2. Inside `card.css` add the following code:

{% tabs %}
{% tab title="card.scss" %}
```css
.card {
  display: flex;
  flex-direction: column;
  position: relative;
  max-width: 420px;
  box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
}

.card img {
  display: block;
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
}

.card__tag--link:hover,
.card__tag--link:focus {
  color: lighten(#1a202c, 25%);
}

/* ========== Card wide styles========= */
.card.card__wide {
  box-shadow: none;
  border: 1px solid #ccc;
  flex-direction: column;
}

.card__wide .card__body-text {
  margin-bottom: 40px;
}

/* Changes card layout on larger screens. */
@media screen and (min-width: 640px) {
  .card.card__wide {
    flex-direction: row;
    max-width: 720px;
  }

  .card__wide .card__media,
  .card__wide .card__content {
    flex: 0 0 50%;
  }

  .card__wide .card__content {
    padding: 40px 20px 20px 40px;
  }
}

```
{% endtab %}
{% endtabs %}

#### Add the new CSS file to Pattern Lab

Just like we've done with previous components, let's add our new card.css to Pattern Lab so the card looks styled.

1. In your text editor, open `source/_meta/_00-head.twig`
2. Copy one of the lines of code that start with `<link...>` which are typically located at the top of the page, and paste it directly after the last item that starts with `<link ...>`
3. Change the path in the newly copied file to be `../../css/card.css`
4. Save the file.

#### Compiling the code

After saving the changes above Pattern Lab should had reloaded. If not run:

```text
npm start
```

