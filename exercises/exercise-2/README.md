# Exercise 2

## Hero

The Hero component is a more complex component because it contains more fields, logic and it also makes use of previously built components. With the Hero we will reuse other components by using twig's [include](https://twig.symfony.com/doc/2.x/tags/include.html) statements. More on this later.

Whether you are building simple or complex components, the process for getting started is the same; create files for data, markup and styles. Let's do this with the Hero component.

First let's identify the data fields we need.

![Hero component](../../.gitbook/assets/hero.png)

Based on the design above, we need the following fields:

* **title or heading \(**Leveling Up\)
* **image**
* **call to action \(CTA\)**

### Building the component

{% hint style="info" %}
**Atomic Design**

We will build the Hero by combining previously built components. This makes the Hero a Molecule, as it will combine several Atoms \(each of the fields above is an Atom\).
{% endhint %}

#### Component's stock content

1. Inside `source/_patterns/01-molecules/` create a new directory called **hero**
2. Inside the _hero_ directory create a new file called **hero.json**
3. Inside `hero.json` add the following code:

{% tabs %}
{% tab title="hero.json" %}
```yaml
{
  "image": "<img src='https://source.unsplash.com/DOoYFgTQWfs/1900x700' alt='Books on computer' />",
  "heading": {
    "heading_level": "1",
    "modifier": "hero__title heading--large",
    "title": "Leveling Up",
    "url": ""
  },
  "cta": {
    "text": "Get started",
    "url": "#"
  }
}
```
{% endtab %}
{% endtabs %}

Just as we did with the Heading component, we are using JSON to define the component's fields, and add stock/dummy content for the component.

#### Some things to notice: <a id="some-things-to-notice"></a>

* The`heading` and `cta` fields were declared as JSON objects with `key|value`pair properties within them. This can be helpful when nesting components.  More on this later.
* All the fields as well as the entire hero component provide a `modifier` key, this is handy because we can use the `modifier` key to pass a CSS class if we need to do some special styling for any of the items in the hero.

#### Component's Markup

Now let's write some HTML for the component.

1. Inside the _hero_ directory create a new file called **hero.twig**
2. Inside `hero.twig` add the following code:

{% tabs %}
{% tab title="hero.twig" %}
```php
<section class="hero">
  {% if image %}
    <div class="hero__media">
      {{ image }}
    </div>
  {% endif %}

  <div class="hero__content">
    {% if heading %}
      {%
        include '@atoms/heading/heading.twig' with {
          "heading_level": heading.heading_level,
          "modifier": heading.modifier,
          "title": heading.title,
          "url": ""
        } only
      %}
    {% endif %}

    {% if cta %}
      <a href="{{ cta.url }}" class="button hero__cta">
        {{ cta.text }}
      </a>
    {% endif %}
  </div>
</section>
```
{% endtab %}
{% endtabs %}

#### Some things to notice: <a id="some-things-to-notice-1"></a>

* We're starting off with a `<section>` HTML5 tag. Learn more about the [section](https://www.w3schools.com/tags/tag_section.asp) tag. This is the parent selector of the component and therefore it should be named **hero**. We do this by using the CSS class of `hero`.  This also establishes the namespace for the component.
* For each field we want to print, we first check if there is content to print using a Twig conditional statement \(`if`\). This is a good practice so we don't print empty HTML elements.
* Notice how every field uses a CSS class that starts with `hero__*`. Defining relationships between the parent elements and child elements by using the same namespace \(hero\_\_\), makes it easier to identify elements when inspecting code as well as finding those elements in our project.
* **Lastly, and super important**, we make use of Twig's `include` statement to include or nest the Heading component. This is extremely powerful and we will be talking more about it later. Biggest benefit of include statements is that we can reuse other components to avoid duplicating code.  Learn more about **Twig includes** in the next page.

#### Component's styles

1. Inside the `source/css` directory create a new file called **hero.css**
2. Inside `hero.css` add this code:

{% tabs %}
{% tab title="hero.css" %}
```css
.hero {
  position: relative;
}

.hero img {
  display: block;
}

.hero__content {
  position: absolute;
  text-align: center;
  top: 45%;
  width: 100%;

}

.hero__content h1 {
  color: #ffffff;
  margin-bottom: 40px;
}
```
{% endtab %}
{% endtabs %}

The advantage of using custom CSS classes on our elements is that our CSS becomes extremely simple and flat as a result. This is a good thing as it makes it easier to maintain and override. The CSS classes we have assigned to the elements use the [BEM methodology](https://css-tricks.com/bem-101/).

#### Add the new CSS file to Pattern Lab

Out of the box Pattern Lab does not have a system to become aware of new CSS stylesheets that are created. This is a manual process which is not complicated at all. However, on a typical project this should be an automated process. We will implement a basic system to automate this process later on. For now follow these steps to make Pattern Lab aware of the new `hero.css` stylesheet.

1. In your text editor, open `source/_meta/_00-head.twig`
2. Copy one of the lines of code that starts with `<link.../>` which are typically located at the top of the page, and paste it directly after the last item that starts with `<link ...>`
3. Change the path in the newly copied file to be `../../css/hero.css`
4. Save the file.

### Compiling the code

Now that the Hero component is done, let's compile the code so we can see it in Pattern Lab. If you already have Pattern Lab running you should see the new Hero component under the Molecules dropdown. Otherwise, run the following command in your command line and press **Return**

```bash
npm start
```

