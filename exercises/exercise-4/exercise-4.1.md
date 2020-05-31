# Exercise 4.1

## Blog Content List

Now build the next list of content as shown in the image below.

* Repeat the same steps as the Featured Content List
* In `data.json` use the object name of `blog`
* Remember some of the fields in the Blog list cards are different and the cards use the "Card wide" variant.

![Our Blog List](../../.gitbook/assets/components-for-beginners-blog.png)

{% tabs %}
{% tab title="data.json" %}
```yaml
{
  "heading": {
    "heading_level": "2",
    "modifier": "heading--large center section-header",
    "title": "From our blog",
    "url": ""
  },
  "cta": {
    "modifier": "",
    "text": "See more articles",
    "url": "#"
  },
  "items": [
    {
      "image": "<img src='https://source.unsplash.com/qQGAQMbURhU/640x360' alt='Man doing yoga' />",
      "title": {
        "heading_level": "3",
        "modifier": "card__title",
        "title": "The beauty of nature",
        "url": "#"
      },
      "date": "March 16 2020",
      "body_text": "Curabitur blandit tempus porttitor. Vestibulum id ligula porta felis euismod semper. Vivamus sagittis lacus vel augue laoreet rutrum faucibus dolor auctor.",
      "tags": [
        {
          "name": "Phtography",
          "url": "#"
        },
        {
          "name": "Nature",
          "url": "#"
        },
        {
          "name": "Outdors",
          "url": "#"
        }
      ],
      "modifier": "from-our-blog__card"
    },
    {
      "image": "<img src='https://source.unsplash.com/HONJP8DyiSM/640x360' alt='Tech gadgets' />",
      "title": {
        "heading_level": "3",
        "modifier": "card__title",
        "title": "The beauty of nature",
        "url": "#"
      },
      "date": "March 16 2020",
      "body_text": "Curabitur blandit tempus porttitor. Vestibulum id ligula porta felis euismod semper. Vivamus sagittis lacus vel augue laoreet rutrum faucibus dolor auctor.",
      "tags": [
        {
          "name": "Phtography",
          "url": "#"
        },
        {
          "name": "Nature",
          "url": "#"
        },
        {
          "name": "Outdors",
          "url": "#"
        }
      ],
      "modifier": "from-our-blog__card"
    },
    {
      "image": "<img src='https://source.unsplash.com/4b9Talfia6c/640x360' alt='Candy in shape of heart' />",
      "title": {
        "heading_level": "3",
        "modifier": "card__title",
        "title": "The beauty of nature",
        "url": "#"
      },
      "date": "March 16 2020",
      "body_text": "Curabitur blandit tempus porttitor. Vestibulum id ligula porta felis euismod semper. Vivamus sagittis lacus vel augue laoreet rutrum faucibus dolor auctor.",
      "tags": [
        {
          "name": "Phtography",
          "url": "#"
        },
        {
          "name": "Nature",
          "url": "#"
        },
        {
          "name": "Outdors",
          "url": "#"
        }
      ],
      "modifier": "from-our-blog__card"
    },
    {
      "image": "<img src='https://source.unsplash.com/hn6CC9aosEk/640x360' alt='Painting of a tiger' />",
      "title": {
        "heading_level": "3",
        "modifier": "card__title",
        "title": "The beauty of nature",
        "url": "#"
      },
      "date": "March 16 2020",
      "body_text": "Curabitur blandit tempus porttitor. Vestibulum id ligula porta felis euismod semper. Vivamus sagittis lacus vel augue laoreet rutrum faucibus dolor auctor.",
      "tags": [
        {
          "name": "Phtography",
          "url": "#"
        },
        {
          "name": "Nature",
          "url": "#"
        },
        {
          "name": "Outdors",
          "url": "#"
        }
      ],
      "modifier": "from-our-blog__card"
    }
  ]
}
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="blog-content.twig" %}
```php
{{ attach_library('training_theme/from-our-blog') }}

<section class="from-our-blog{{ modifier ? ' ' ~ modifier }}{{- attributes ? ' ' ~ attributes.class -}}"
  {{- attributes ? attributes|without(class) -}}>
  {{ title_prefix }}
  {{ title_suffix }}
  {%
    include '@training_theme/heading/heading.twig' with {
      "heading": heading
    } only
  %}

  <div class="from-our-blog__items">
    {% block blog_items %}
      {% for item in items %}
        {% embed '@training_theme/card/card.twig' with
          {
            "image": item.image,
            "title": item.title,
            "date": item.date,
            "body_text": item.body_text,
            "tags": item.tags,
            "modifier": item.modifier
          } only
        %}
          {% block featured_date %}
          {# Purposely leaving empty. #}
          {% endblock featured_date %}
        {% endembed %}
      {% endfor %}
    {% endblock blog_items %}
  </div>
  <div class="from-our-blog__cta">
    {%
      include '@training_theme/button/button.twig' with {
        button: cta
      } only
    %}
  </div>
</section>
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="blog-content.scss" %}
```css
// Import site utilities
@import '../../global/utils/init';

.from-our-blog  {
  max-width: 1440px;
  padding: 0 20px;

  @media screen and (min-width: $bp-xl) {
    padding: 0;
  }
}

// On mobile the cards are displayed
// vertically as a group.
.from-our-blog__items {
  align-items: center;
  display: flex;
  flex-direction: column;

  // On larger screens cards are displayed
  // horizontally as a group.
  @media screen and (min-width: $bp-sm) {
    flex-direction: row;
    justify-content: space-between;
    flex-wrap: wrap;
  }
}

.from-our-blog__card {
  margin-bottom: 60px;

  @media screen and (min-width: $bp-sm) {
    flex: 0 0 45%;
  }

  @media screen and (min-width: $bp-lg) {
    flex: 0 0 22%;
    margin-bottom: 0;
  }
}

.from-our-blog__cta {
  margin: 50px auto 0;
  text-align: center;
}
```
{% endtab %}
{% endtabs %}

### Challenge:  Find ways to improve the styles

Since Featured Content and Blog Content use similar styles, find ways in which you can improve the code to avoid repetition.

