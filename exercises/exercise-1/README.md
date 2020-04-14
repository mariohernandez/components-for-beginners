# Exercise 1

## Heading Component

Following the [Atomic Design ](https://atomicdesign.bradfrost.com/table-of-contents/)methodology we are going to build a simple component or pattern. The Heading pattern is an atom which prints a string of text as the title for a page, paragraph, or other component.

### Component's stock content

Let's start by first identifying the content for the component. Since this is a title field, we only need a string of text. We'll dive into more complex components in future exercises.

{% hint style="info" %}
**NOTE:** All components will be created inside `source/_patterns/ (`i.e. `source/_patterns/00-atoms/heading/)`
{% endhint %}

1. Inside `source/_patterns/00-atoms/` create a new directory called **heading**
2. Inside the _heading_ directory create a new file called **heading.twig**
3. Inside `heading.twig` add the following code:

{% tabs %}
{% tab title="heading.twig" %}
```php
<h1 class="heading">{{ title }}</h1>
```
{% endtab %}
{% endtabs %}

We created a **h1** heading in which we pass the value of `{{ title }}`, but you may ask yourself, what is title and where is it coming from?

#### Pattern Lab's Data

Out of the box Pattern Lab provides sample or stock content for patterns or components.  This is a great way to add content to your components by simply declaring the variable name for the content you need.  In the example of the **heading** component above, we created a H1 and as its value we declared a twig variable of `{{ title }}`.  If we look inside `source/_data` you will see `data.json`.  If you open this file in your text editor you will the very first item in the long list of items, is `title: "Pattern Lab"`.Pattern Lab has been built so by default it looks in the **data.json** file to see if what we are asking to print on the page exists in this file.  If it finds a matching variable name, it will use it.  Later we will learn how to create own own data files so we can be more specific as to what content we want to use in our components.

{% hint style="info" %}
Learn more about [Pattern Lab's Data](https://patternlab.io/docs/data-overview.html)
{% endhint %}

### Compiling the code

Now that the Heading component is done, let's compile the code so we can see it in Pattern Lab.  If you had the `npm start` command running you don't need to do anything else as this commands watches for any changes you make to your css, twig or json, and it autoomatically compiles the changes for you.  In addition, it even reloads the web browser so you can see your changes.

If Pattern Lab was not running, go into the directory of your project \(example: `components_project`\), and run this command, and press **Return:**

`npm start`

Pattern Lab will open and if you look in the **Atoms** dropdown in the main navigation, you should see the **Heading** component at the bottom of the list. The test for the Heading should read "**Pattern Lab".**

### **BONUS:**

* Open `source/_data/data.json` and edit the value of `title` to read "_My website titl_e"
* Save the file and Pattern Lab should reload your browser.  Now your Heading component's text shoudl read "_My website title_".

