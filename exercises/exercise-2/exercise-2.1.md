# Exercise 2.1

## Button component

![Button component](../../.gitbook/assets/components-for-beginners-button.png)

Buttons are some of those things that are used over and over on a website. For this reason it makes sense to create a new atom for the button.

1. Inside `source/_patterns/00-atoms/` create a new directory called **button**
2. Inside the _button_ directory create a new file called **button.json**
3. Inside `button.json` add the following code:

{% tabs %}
{% tab title="button.json" %}
```yaml
{
  "button": {
    "text": "button",
    "url": "",
    "modifier": ""
  }
}
```
{% endtab %}
{% endtabs %}

We created an object called `button` and added several properties or attributes such as `text`, `url`, and `modifier`. By now we've seen this kind of data structure on other components.

If you are wondering why we are nesting all the button properties inside a **button** object instead of writing everything on its own as we did with **heading.json** in the previous exercise.  This sometimes is a personal preference or it could also be a hard data requirement.  I personally like to use objects as we've done above as this helps in two ways:

1. It simplifies the component nesting process by not having to map or associate each individual property when we use includes.  You'll see what I mean shortly,
2. If we are creating components or pages where we are reusing several other components, we may run into the issue of components using the same property names.  If this is the case we would need to change property names as JSON will not allow us to use the same key name more than once.  Using objects to nest the properties solves this issue.

### Writing the button's logic

1. Inside the _button_ directory create a new file called **button.twig**
2. Inside `button.twig` add the following code:

{% tabs %}
{% tab title="button.twig" %}
```php
{% if button.url %}
  <a href="{{ button.url }}" class="button{{ button.modifier ? ' ' ~ button.modifier }}">
    {{ button.text }}
  </a>
  {% else %}
  <button class="button{{ button.modifier ? ' ' ~ button.modifier }}">
    {{ button.text }}
  </button>
{% endif %}
```
{% endtab %}
{% endtabs %}

* We've added some logic to the button to ensure we render the right HTML element based on the data we receive. For example, if a URL is passed, we use an `<a>` tag with the class of **button**, otherwise we use a `<button>` tag. We always want to make sure we use proper semantic markup for accessibility and for the task at hand. An `<a>` tag will allow us to link to another page or a section within the same page, whereas a `<button>` element will allow us to perform an action such as submit content.

### Button Styles

1. Inside the `source/css` directory create a new file called **button.css**
2. Inside `button.css` add the following code:

{% tabs %}
{% tab title="button.css" %}
```css
.button {
  background-color: #003954;
  border: 2px solid #003954;
  color: #ffffff;
  display: inline-block;
  font-size: 16px;
  line-height: 1.3;
  padding: 15px 40px;
  text-transform: uppercase;
  text-decoration: none;
}

.button:hover,
.button:focus {
  color: #ffffff;
}

.button.button--ghost {
  background-color: transparent;
  border: 2px solid #444444;
  color: #444444;
  padding: 8px 30px;
}

.button.button--ghost:hover {
  color: #444444;
}
```
{% endtab %}
{% endtabs %}

* Some basic css styles to make our button look decent.  We can probably improve them but for now they will do.

#### Add the new CSS file to Pattern Lab

1. In your text editor, open `source/_meta/_00-head.twig`
2. Add the following line at the top of the file \(directly after other similar lines\), and Save the file.

{% tabs %}
{% tab title="\_00-head.twig" %}
```markup
<link rel="stylesheet" href="../../css/button.css?{{ cacheBuster }}" media="all" />
```
{% endtab %}
{% endtabs %}

_We added a link to the new CSS file we created for the Button component.  This will ensure any styles we write for the button will be available in Pattern Lab._

### Compiling the code

Now that the Button component is done, let's compile the code so we can see it in Pattern Lab. If you already have Pattern Lab running you should see the new Button component under the Molecules dropdown. Otherwise, run the following command in your command line and press **Return**

```bash
npm start
```

If you look under Atoms in Pattern Lab's main navigation, you should see the Button component at the bottom of the atoms list.

### Next:  Update the Hero to make use of the new button atom
