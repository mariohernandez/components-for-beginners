# Twig Basics

### What is Twig?

Twig is a modern template engine for PHP.  The syntax is easy to learn and has been optimized to allow web designers to get their job done fast without getting in their way.

In this training we will use Twig to write the component's markup \(HTML\).  You may wonder; Why not use HTML instead?  Twig provides the ability to write logic for the markup we write, something HTML does not do.  For example, with Twig we could write something that could be interpreted as this: "**If this field does not have content, show a message to the user**" or, "**Only show 5 items from this array even if there are more**" 

When building compnents we will create Twig templates.  A template is a regular text file. It can generate any text-based format \(HTML, XML, CSV, etc.\). It uses the extension of `.twig` \(i.e. `header.twig`\).

Below is a minimal template that illustrates a few basics. We will cover further details later on.

```php
<!DOCTYPE html>
<html>
    <head>
        <title>My Webpage</title>
    </head>
    <body>
        <ul class="navigation">
        {% for item in navigation %}
            <li><a href="{{ item.href }}">{{ item.text }}</a></li>
        {% endfor %}
        </ul>

        <h1>{{ page_title }}</h1>
    </body>
</html>
```

* There are two kinds of delimiters: `{% ... %}` and `{{ ... }}`. The first one is used to execute statements such as for-loops or conditional statements such as `if` `then`, the latter outputs the result of an expression or variable.
* Notice how the example above includes both, Twig code as well as HTML.  This is what makes Twig easy to read and understand as it provides a familiar syntax and markup structure.

### Variables

In the context of this training JSON passes variables to the Twig templates for manipulation in the template.

```php
{{ page_title }}
```

The example above show how we can render the value of the **page\_title** key from a JSON file.

### Statements

Whenever we need to conduct some kind of logic or expression, we use the `{% ... %}` delimiter.  Let's see an example:

```php
<ul class="navigation">
  {% for item in navigation %}
    <li><a href="{{ item.href }}">{{ item.text }}</a></li>
  {% endfor %}
</ul>
```

* In the example above we are building a menu or navigation.  We're starting by writing an unordered list \(`<ul>`\).  Then we create a `for` loop statement \(`{% for item in navigation %}`\).  This means that we probably have an array in JSON called `navigation` which may have multiple tiems in it.  The statement above is saying:  "**for every** `item` **found in the** `navigation` **array, we will create a list item \(**`<li>`**\) and within it we will add a link**".

As you can see Twig's syntax is simple and easy to follow.   During this training we will be writing similar statements as the examples above.  We will keep twig code as basic as possible.

{% hint style="info" %}
Learn [more about Twig ](https://twig.symfony.com/doc/2.x/templates.html)as this will be essential to follow along during this training.
{% endhint %}

