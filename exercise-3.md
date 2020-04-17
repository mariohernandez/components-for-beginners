# Exercise 3

## Hero

The Hero component is a more complex component because it contains more fields, logic and it also makes use of previously built components. With the Hero we will reuse other components by using twig's [include](https://twig.symfony.com/doc/2.x/tags/include.html) statements. More on this later.

Whether you are building simple or complex components, the process for getting started is the same; create files for data, markup and styles. Let's do this with the Hero component.

First let's identify the data fields we need.

![Hero component  \(picture from https://unsplash.com by Aniket Deole\)](.gitbook/assets/components-for-beginners-hero.png)

Based on the design above, we need the following fields:

* **title or heading**: "Leveling Up"
* **image**: Yosemite
* **call to action \(cta\)**: "Get started"

### Building the component

{% hint style="info" %}
**Atomic Design**

We will build the Hero by combining previously built components.  This makes the Hero a Molecule, as it will combine several Atoms \(each of the fields above is an Atom\).
{% endhint %}

#### Component's stock content

1. Inside `source/_patterns/01-molecules/` create a new directory called **hero**
2. Inside the _hero_ directory create a new file called **hero.json**
3. Inside `hero.json` add the following code:

{% tabs %}
{% tab title="hero.json" %}
```yaml
{
  "image": "<img src='https://source.unsplash.com/M6XC789HLe8/1600x700' alt='A wonderful image' />",
  "heading": {
    "heading_level": "1",
    "modifier": "hero__title",
    "title": "Leveling Up",
    "url": ""
  },
  "cta": {
    "text": "Get started",
    "url": "#",
    "modifier": "hero__cta"
  },
  "modifier": ""
}
```
{% endtab %}
{% endtabs %}

Just as we did with the Heading component, we are using JSON to define the component's fields, and add stock/dummy content to the component. 

#### Some things to notice: <a id="some-things-to-notice"></a>

* The`heading` and `cta` fields were declared as JSON objects with `key|value`pair properties within them. Typically these object's data structure matches the original components. For example, if you look at the data structure for the **Heading** component you will see it is the same as what we have here in the Hero. When component's data structures match it makes it easier to nest components into other components. More on this later.
* All the fields provide a `modifier` key \(i.e. `hero__*`\). This is handy because it establishes a relationship between child and parent elements \(using the [BEM](https://css-tricks.com/bem-101/) methodology\), but it also facilitates styling those elements differently than the original components.

#### Component's Markup

Now let's write some HTML for the component.

1. Inside the _hero_ directory create a new file called **hero.twig**
2. Inside `hero.twig` add the following code:

{% tabs %}
{% tab title="hero.twig" %}
```php
<section class="hero{{ modifier ? ' ' ~ modifier }}">
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
          "title": heading.title,
          "url": "",
          "modifier": heading.modifier
        } only
      %}
    {% endif %}

    {% if cta %}
      <a href="{{ cta.url }}" class="{{ cta.modifier }}">
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
* For each field we want to print, we first check if there is content to print using a Twig conditional statement \(`if`\). This is a good practice so we don't print empty HTML.
* Notice how every field uses a CSS class that starts with `hero__*`. Defining relationships between the parent elements and child elements by using the same namespace \(hero\_\_\), makes it easier to identify elements when inspecting code as well as finding those elements in our project.
* **Lastly, and super important**, we make use of Twig's `include` statement to include or nest previously built components into the Hero. This is extremely powerful and we will be talking more about it later. Biggest benefit of include statements is that we can reuse other components to avoid duplicating code.

#### Component's styles

1. Inside the _hero_ directory create a new file called **hero.css**
2. Inside `hero.css` add this code:

{% tabs %}
{% tab title="hero.css" %}
```css
.hero {
  position: relative;
}

.hero::before {
  background: linear-gradient(to top,#222222 0 5%,transparent 40% 100%);
  bottom: 0;
  content: '';
  display: block;
  left: 0;
  position: absolute;
  right: 0;
  top: 0;
}

.hero img {
  display: block;
}

.hero__content {
  position: absolute;
  text-align: center;
  top: 35%;
  width: 100%;

}

.hero__content h1 {
  color: #ffffff;
  font-family: Arial, Helvetica, sans-serif;
  font-size: 110px;
  font-weight: 900;
  margin-bottom: 40px;
  text-transform: uppercase;
}

.hero__cta {
  background-color: transparent;
  border: 2px solid #ffffff;
  color: #ffffff;
  display: inline-block;
  font-size: 24px;
  font-weight: bold;
  line-height: 1.3;
  padding: 12px 40px;
  text-decoration: none;
  text-transform: uppercase;
}

.hero__cta:hover {
  color: #ffffff;
}

```
{% endtab %}
{% endtabs %}

The code above simply imports global utilities from our theme which will be needed as we start writing styles in Sass. More on this later.

#### Add the new CSS file to Pattern Lab

1. In your text editor, open `source/_meta/00-head.twig`
2. Copy one of the lines of code that start with `<link...>` which are typically located at the top of the page, and paste it directly after the last item that starts with `<link ...>`
3. Change the path in the newly copied file to be `../../css/scss/components/hero.css`
4. Save the file.

### Compiling the code <a id="compiling-the-code"></a>

Now that the Hero component is done, let's compile the code so we can see it in Pattern Lab.  If you already have Pattern Lab running you should see the new Hero component.  Otherwise, run the following command in your command line and press **Return**

`npm start`

