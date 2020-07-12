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
    "modifier": "heading--large center section-header",
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
      "image": "<img src='https://source.unsplash.com/m6OZNfmo2Dk' alt='Man doing yoga' />",
      "title": {
        "heading_level": "3",
        "modifier": "blog-content__title",
        "title": "Staying healthy",
        "url": ""
      },
      "date": "",
      "category": "Fashion",
      "body_text": "Curabitur blandit tempus porttitor. Vestibulum id ligula porta felis euismod semper. Vivamus sagittis lacus vel augue laoreet.",
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
      "body_text": "Curabitur blandit tempus porttitor. Vestibulum id ligula porta felis euismod semper. Vivamus sagittis lacus vel augue laoreet.",
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
@import '../../../css/scss/generic/variables';

.blog-content  {
  max-width: 1440px;
  padding: 0 20px;

  @media screen and (min-width: $bp-xxl) {
    padding: 0;
  }
}

// On mobile cards are displayed
// vertically as a group.
.blog-content__items {
  align-items: center;
  display: flex;
  flex-direction: column;

  // On larger screens cards are displayed
  // horizontally as a group.
  @media screen and (min-width: $bp-xxl) {
    flex-direction: row;
    justify-content: space-between;
  }
}

.blog-content__card {

  @media screen and (min-width: $bp-large) {
    flex: 0 0 45%;
    margin-bottom: 0;
  }
}

// Adds spacing between cards on mobile, except
// the last card.
.blog-content__card:not(:last-child) {
  margin-bottom: 60px;

  @media screen and (min-width: $bp-xxl) {
    margin-bottom: 0;
  }
}

.blog-content__cta {
  margin: 50px auto 0;
  text-align: center;
}
```
{% endtab %}
{% endtabs %}

### Challenge:  Find ways to improve the styles

Since Featured Content and Blog Content use similar styles, find ways in which you can improve the code to avoid repetition.

