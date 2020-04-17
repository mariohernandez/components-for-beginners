# Twig Basics

Twig is a modern template engine for PHP.  The syntax is easy to learn and has been optimized to allow web designers to get their job done fast without getting in their way.

This document describes the syntax and semantics of the template engine and will be most useful as we create Twig templates. A template is a regular text file. It can generate any text-based format \(HTML, XML, CSV, LaTeX, etc.\). It doesn’t have a specific extension, `.html` or `.xml` are just fine.

A template contains **variables** or **expressions**, which get replaced with values when the template is evaluated, and **tags**, which control the template’s logic.

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

        <h1>My Webpage</h1>
        {{ a_variable }}
    </body>
</html>
```

There are two kinds of delimiters: `{% ... %}` and `{{ ... }}`. The first one is used to execute statements such as for-loops, the latter outputs the result of an expression or variable.

Notice how the example above includes both, Twig code as well as HTML.  This is what makes Twig easy to read and understand as it provides a familiar syntax and markup structure.

### Variables

In the context of this training JSON passes variables to the Twig templates for manipulation in the template. Variables may have attributes or elements you can access, too. 

```php
{{ name }}
```

The example above show how we can render the value of the **name** key from a JSON file.

### Statements

Whenever we need to conduct some kind of logic or expression, we use the `{% ... %}` delimiter.  Let's see an example:

```php
<ul class="navigation">
  {% for item in navigation %}
    <li><a href="{{ item.href }}">{{ item.text }}</a></li>
  {% endfor %}
</ul>
```

In the example above we are building a menu or navigation.  We're starting by writing an unordered list \(`<ul>`\).  Then we create a for loop statement \(`{% for item in navigation %}`\).  This means that for every item found in the navigation array, we will create a list item \(`<li>`\) and within it we will add a link.

As you can see Twig's syntax is simple and easy to follow.   During this training we will be writing similar statements as the examples above.  We will keep twig code to a minimum.

{% hint style="info" %}
Learn [more about Twig ](https://twig.symfony.com/doc/2.x/templates.html)as this will be essential to follow along during this training.
{% endhint %}

