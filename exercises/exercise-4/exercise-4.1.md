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
"blog": {
  "heading": {
    "heading_level": "2",
    "modifier": "heading--large",
    "title": "From our blog",
    "url": ""
  },
  "cta": {
    "modifier": "",
    "text": "Load more articles",
    "url": ""
  },
  "items": [
    {
      "image": "<img src='https://source.unsplash.com/qQGAQMbURhU/260x360' alt='Man doing yoga' />",
      "title": {
        "heading_level": "3",
        "modifier": "blog-content__title",
        "title": "Staying healthy",
        "url": ""
      },
      "date": "",
      "category": "Fashion",
      "body_text": "Curabitur blandit tempus porttitor. Vestibulum id ligula porta felis euismod semper. Vivamus sagittis lacus vel augue laoreet rutrum faucibus dolor auctor. Aenean lacinia bibendum nulla sed consectetur.",
      "tags": "",
      "cta": {
        "modifier": "blog-content__cta button--ghost",
        "text": "Read the full article",
        "url": "#"
      },
      "modifier": "blog-content__card card--wide"
    },
    {
      "image": "<img src='https://source.unsplash.com/HONJP8DyiSM/260x360' alt='Tech gadgets' />",
      "title": {
        "heading_level": "3",
        "modifier": "blog-content__title",
        "title": "Tech gadgets",
        "url": ""
      },
      "date": "",
      "category": "Sports",
      "body_text": "Curabitur blandit tempus porttitor. Vestibulum id ligula porta felis euismod semper. Vivamus sagittis lacus vel augue laoreet rutrum faucibus dolor auctor. Aenean lacinia bibendum nulla sed consectetur.",
      "tags": "",
      "cta": {
        "modifier": "blog-content__cta button--ghost",
        "text": "Read the full article",
        "url": "#"
      },
      "modifier": "blog-content__card card--wide"
    }
  ]
}
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="blog-content.twig" %}
```php
<section class="blog-content">
  {% include '@atoms/heading/heading.twig' with {
      heading: blog.heading
    } only
  %}

  <div class="blog-content__items">
    {% for item in blog.items %}
      {%
        include '@molecules/card/card.twig' with {
          "image": item.image,
          "title": item.title,
          "category": item.category,
          "body_text": item.body_text,
          "cta": item.cta,
          "modifier": item.modifier
        } only
      %}
    {% endfor %}
  </div>

  {% if blog.cta %}
    <div class="blog-content__cta">
      {%
        include '@atoms/button/button.twig' with {
          button: blog.cta
        } only
      %}
    </div>
  {% endif %}
</section>


```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="blog-content.scss" %}
```css
@import '../../../css/scss/generic/mixins';

.blog-content  {
  max-width: 1440px;
  margin: 0 auto;
}

.blog-content__items {
  display: flex;
  justify-content: space-between;
  margin-bottom: 40px;
}

.blog-content__card {
  flex: 0 0 48%;
}

.blog-content__cta {
  margin: 10px auto 0;
  text-align: center;
}

// This can be placed elsewhere.
.footer {
  margin-top: 80px;
  background-color: #000000;
  height: 100px;
}
```
{% endtab %}
{% endtabs %}

