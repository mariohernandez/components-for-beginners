# Exercise 5

## Homepage prototype

![Homepage](../../.gitbook/assets/components-for-beginners.png)

It is now time to put all the pieces together to build the homepage shown above. Building prototype pages in Pattern Lab is a great way to demo to stakeholders and team members the end product of a project. This is particularly useful for testing.

Building the page will be relatively easy because all we need to do is include all the components we already built. Since we already created sample data in `data.json` for the Featured Content and Blog Content sections in the previous two exercises, we can reuse it for the homepage. We just need to add data for the Hero component in `data.json`. Let's do that now.

### Demo content

1. In your text editor open `source/_data/data.json`
2. Scroll to the end of the file and before the last curly bracket \( } \), add a comma and press **Return**
3. Copy the code below and paste it in the empty space you just created in the previous step.  Ensure the indentation of the newly added code matches the current indentation in the file. 

{% tabs %}
{% tab title="data.json" %}
```yaml
"hero_new": {
  "image": "<img src='https://source.unsplash.com/M6XC789HLe8/1900x700' alt='Yosemite' />",
  "heading": {
    "heading_level": "1",
    "modifier": "hero__title heading--large",
    "title": "Leveling Up",
    "url": ""
  },
  "cta": {
    "text": "Get started",
    "url": "#",
    "modifier": "hero__cta"
  }
}
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
**WARNING**: Ensure you are using/matching the file's indentation preferences for code \(i.e. 2 spaces\). In addition, as we saw in the [JSON Basics](../../basics/json-basics.md) section, ensure you adhere to JSON's punctuation rules \(i.e. commas between each data objects except on the last item.
{% endhint %}

* As you can see above, we are creating an object for the Hero component called **hero\_new**.  Why hero\_new? you may ask yourself.  If you look in `data.json` you will find that there is a `hero:` key.  Rather than overriding the existing key and risking breaking patterns that may already be using it, we're starting with a new object.
* The data structure above was copied from the Hero component we built.

### Building the Twig template for homepage

Now that we have all the data we need, let's build the Twig template that will become our new homepage. As we did with the components we built, we will be using our own naming convention by excluding the numeric prefixes found in patterns provided by Pattern Lab. This is only a personal preference and you are welcome to use Pattern Lab's naming convention if that suits you better.

### Create the Homepage page

1. Inside `source/_patterns/04-pages/` create a new file called **homepage.twig**
2. In _homepage.twig_ write the following code to add the Hero component to the page:

{% tabs %}
{% tab title="homepage.twig" %}
```php
{%
  include '@molecules/hero/hero.twig' with {
    "image": hero_new.image,
    "heading": hero_new.heading,
    "cta": hero_new.cta
  } only
%}
```
{% endtab %}
{% endtabs %}

* Notice how we are only including the **hero** component and mapping its fields to the fields/keys in `data.json`.  We are not writing any HTML.  

If you save your changes and you have Pattern Lab running you should see Homepage in Pattern Lab's "Pages" dropdown \(it should be at the bottom of the list\).  Clicking Homepage should display a new page with a hero in it.

If Pattern Lab was not running run `npm start` to start it.

### Adding the Featured Content List component

When we built the Featured Content List component we added its data to `data.json`. This means we don't have to do anything for data for the homepage.  We can use the same data we already created. All we have to do now is include that component in `homepage.twig` and map its fields accordingly.

1. In _homepage.twig_ write the following code and save your changes:
2. For readability, you may want to leave an empty line in between each component's include.

{% tabs %}
{% tab title="homepage.twig" %}
```php
{% include '@organisms/featured-content/featured-content.twig' %}
```
{% endtab %}
{% endtabs %}

This include statement above is much different and simpler. Since the data for Featured Content List was originally created in `data.json`, Pattern Lab is smart enough to automatically retrieve all the keys and values. This eliminates the need to map each field as we did with the Hero.

Pattern Lab should now show in addition to Hero, the Featured Content list. Don't worry about the spacing around the components for now. We'll address that shortly.

### Adding the Our Blog List component

{% tabs %}
{% tab title="homepage.twig" %}
```php
{% include '@organisms/blog-content/blog-content.twig' %}
```
{% endtab %}
{% endtabs %}

### Adding the Footer component

We'll keep the footer simple.  Let's quickly modify Pattern Lab's default footer component.

1. In `source/_patterns/02-organisms/` create a new folder called **footer**
2. In the _footer_ directory create a new file called **footer.scss**
3. Add the following code:

{% tabs %}
{% tab title="footer.scss" %}
```css
@import '../../../css/scss/generic/variables';

.footer {
  align-items: center;
  background-color: $navy-blue;
  display: flex;
  justify-content: center;
  padding: 20px 0 5px;

  p {
    margin: 0;
  }

  .visually-hidden {
    position: absolute;
    height: 1px;
    width: 1px;
    overflow: hidden;
    clip: rect(1px, 1px, 1px, 1px);
    white-space: nowrap;
  }
}

.footer__logo svg {
  width: 125px;
  height: auto;
}
```
{% endtab %}
{% endtabs %}

* We're starting with basic styles to enter-align the footer text.
* We're also adding a SVG file for the actual logo, but we're hiding it from screen readers by using `aria-hidden="true"`
* As for the copyright text, we're hiding it from view \(`.visually-hidden`\), but making it available to screen readers for accessibility purposes.

#### Updating Pattern Lab's default footer

1. In your editor, open `source/_patterns/02-organisms/00-global/01-footer.twig`
2. Update the existing code so it looks like this \(_the SVG code is pretty lengthy, be sure to capture it all_\):

{% tabs %}
{% tab title="01-footer.twig" %}
```php
<footer class="footer" role="contentinfo">
	<p class="visually-hidden">&copy; 2020 Mediacurrent Training</p>
	<div class="footer__logo">
		<svg aria-hidden="true" xmlns="http://www.w3.org/2000/svg" width="300" height="300" viewBox="0 0 300 300"><path d="M214.74,44.33c-27.32,0-37.26,19.91-43.35,30.67h-.54c-1.38-15.46-5-30.67-33.13-30.67-25.95,0-36.45,20.73-41.15,29.57H96V44.33L47.44,51v6.09c10.76,0,20.7,2.49,20.7,22.11v26.22c9.55-2.75,19.13-5.21,28.74-7.3,2.56-16.63,12.2-36.89,31.74-36.89,10.66,0,13.73,7.93,14.4,30.43a234.48,234.48,0,0,1,29-.1c.62,0,1.21.12,1.81.17,4.54-14.89,14.81-30.5,29.55-30.5,13.55,0,14.86,8.65,14.91,37.2,9.4,2.06,18.7,4.29,27.89,6.6V92.38c0-30.91-2.21-48-31.48-48Z" fill="#fff"/><path d="M246.22,118.48a.06.06,0,0,0-.07,0c-24.81-6.26-48.38-12.09-74.22-13.7-.13,0-14.92-.37-15.41-.37-51.94.37-104.3,13-155.52,32.75a628.11,628.11,0,0,1,67.14-13.51V144c0,19.06-4.7,24-20.7,24v6.07h66.81V168C100.18,168,96,163.08,96,144V120.3c15.93-1.54,31.74-2.39,47.2-2.44V144c0,19.06-4.14,24-18.22,24v6.07h64.34V168c-14.09,0-18.21-4.95-18.21-24V118.57c15.93,1,31.45,4,47.2,7.58V144c0,19.06-3.88,24-18.24,24v6.07h66.84V168c-16.3,0-20.72-4.95-20.72-24V132.88c11.42,2.85,23.44,5.76,36.1,8.38,12.81,2.67,18-4.31,16.6-9-11.42-2.54-52.7-13.73-52.7-13.73Z" fill="#fff"/><path d="M-.35,224.47c3.09,0,4-1,4-4.64V207.29c0-3.79-1.92-4.27-4-4.27v-1.17L9,200.56v5.71h.11c.91-1.7,2.93-5.71,8-5.71,5.44,0,6.14,2.94,6.4,5.93h.11c1.17-2.08,3.09-5.93,8.38-5.93,5.65,0,6.08,3.31,6.08,9.29v10c0,3.68.85,4.64,4,4.64v1.18H29.16v-1.18c2.77,0,3.52-1,3.52-4.64v-8.54c0-5.76-.21-7.47-2.88-7.47-3.9,0-6.25,5.66-6.25,8.86v7.15c0,3.68.8,4.64,3.53,4.64v1.18H14.64v-1.18c2.72,0,3.52-1,3.52-4.64V212c0-6.19-.42-8.16-2.82-8.16-4.49,0-6.3,5.55-6.3,8.86v7.15c0,3.68.8,4.64,3.52,4.64v1.17H-.35Z" fill="#fff"/><path d="M63.31,224.79a21,21,0,0,1-7.37,1.39c-8.22,0-13.07-4.8-13.07-13.66,0-8.06,4-12,11.15-12,8.38,0,9.77,5.61,9.77,10.09H48.68c0,5.61,2.14,13.13,9.72,13.13a14,14,0,0,0,4.91-.91ZM58.4,208.46c0-3.36-.91-6.08-4.59-6.08-4.06,0-5.13,4-5.13,6.08Z" fill="#fff"/><path d="M84.6,221.81h-.11c-1.18,1.76-3,4.37-7.74,4.37-7.31,0-9-6.56-9-12.81,0-7.2,2.67-12.81,10.09-12.81a7.39,7.39,0,0,1,6.67,3.85h.11v-9.13c0-3.79-1.93-4.27-4-4.27v-1.17l9.4-1.28v30.89c0,3.8,1.86,4.28,4,4.28v1.17l-9.39,1.28Zm-5.39,1.33c4.48,0,5.39-4.64,5.39-9.77,0-6.51-1.23-10.24-5.39-10.24-4.43,0-5.66,5.23-5.66,10.24C73.55,218.87,74.78,223.14,79.21,223.14Z" fill="#fff"/><path d="M95.69,224.47c3.15,0,4-1,4-4.64V207.29c0-3.79-1.92-4.27-4-4.27v-1.17l9.39-1.29v19.27c0,3.68.86,4.64,4,4.64v1.18H95.69Zm3.47-31.59a3.26,3.26,0,0,1,3.31-3.31,3.34,3.34,0,1,1-3.31,3.31Z" fill="#fff"/><path d="M135.45,225.22a16.65,16.65,0,0,1-5.61,1c-3.2,0-3.84-1.87-4.21-3.63a9.65,9.65,0,0,1-7.31,3.63c-3.69,0-7-2.61-7-6.08,0-7.47,10.94-7.95,14.25-8.11v-2.67c0-2.88,0-6.94-3.68-6.94-5.28,0-1.65,6.41-6.51,6.41a2.78,2.78,0,0,1-3-2.73c0-3.84,5.39-5.5,9.76-5.5,6.73,0,8.86,2.68,8.86,8.76v10.62c0,3.25.64,4.43,2.4,4.43a7.53,7.53,0,0,0,2.09-.48v1.33ZM125.57,214c-2,0-8.43.37-8.43,5.39,0,2.08,1.12,3.79,3.36,3.79,3,0,5.07-2.19,5.07-6.08V214Z" fill="#fff"/><path d="M156.15,224.9a16.2,16.2,0,0,1-6.83,1.28c-8.54,0-12.54-5.12-12.54-13.93,0-6.35,2.93-11.69,10.88-11.69,4.16,0,8.65,2.09,8.65,5.5,0,2-1.66,2.88-3.26,2.88-3.25,0-2.88-3.73-3.25-4.8a2.28,2.28,0,0,0-2.56-1.76c-3.31,0-4.65,3.31-4.65,8.75s1.87,12.65,8.81,12.65a17.52,17.52,0,0,0,4.75-.8Z" fill="#fff"/><path d="M177,219.88h-.11c-1.12,2.14-3.41,6.3-8.11,6.3-6,0-7.1-3-7.1-7.1V207.29c0-3.79-1.92-4.27-4-4.27v-1.17l9.39-1.29v14.2c0,6.46,1,8.17,4.06,8.17,2.77,0,5.87-5.56,5.87-8.86v-6.78c0-3.79-1.92-4.27-4-4.27v-1.17l9.39-1.29v18.9c0,3.79,2,4.27,4,4.27v1.17L177,226.18v-6.3Z" fill="#fff"/><path d="M188,224.47c3.1,0,4-1,4-4.64V207.29c0-3.79-1.92-4.27-4-4.27v-1.17l9.39-1.29v6.2h.11c.91-2.41,2.88-6.2,7.26-6.2a2.92,2.92,0,0,1,2.88,2.78,2.83,2.83,0,0,1-2.88,3c-1.93,0-1.55-1.23-3.31-1.23s-4.06,3.26-4.06,8.75v6c0,3.68.91,4.64,4,4.64v1.18H188v-1.18Z" fill="#fff"/><path d="M208.76,224.47c3.09,0,4-1,4-4.64V207.29c0-3.79-1.93-4.27-4-4.27v-1.17l9.39-1.29v6.2h.11c.9-2.41,2.88-6.2,7.25-6.2a2.91,2.91,0,0,1,2.88,2.78,2.83,2.83,0,0,1-2.88,3c-1.92,0-1.55-1.23-3.31-1.23s-4,3.26-4,8.75v6c0,3.68.9,4.64,4,4.64v1.18H208.76v-1.18Z" fill="#fff"/><path d="M251.07,224.79a20.9,20.9,0,0,1-7.36,1.39c-8.22,0-13.08-4.8-13.08-13.66,0-8.06,4-12,11.16-12,8.37,0,9.76,5.61,9.76,10.09h-15.1c0,5.61,2.13,13.13,9.71,13.13a13.86,13.86,0,0,0,4.91-.91Zm-4.91-16.33c0-3.36-.91-6.08-4.59-6.08-4.06,0-5.12,4-5.12,6.08Z" fill="#fff"/><path d="M254.48,224.47c3.1,0,4-1,4-4.64V207.29c0-3.79-1.93-4.27-4-4.27v-1.17l9.39-1.29v6.3H264c1.23-2.19,3.69-6.3,8.75-6.3,5.45,0,6.46,3.05,6.46,7.1v12.17c0,3.68.91,4.64,4,4.64v1.18H269.8v-1.18c3.09,0,4-1,4-4.64V212c0-6.46-.8-8.17-3.41-8.17-3.1,0-6.52,5.55-6.52,8.86v7.15c0,3.68.91,4.64,4,4.64v1.18h-13.4Z" fill="#fff"/><path d="M298.77,225.59a8.43,8.43,0,0,1-3,.59c-4.7,0-8.65-.75-8.65-7v-15.9h-4.32v-1.5c6.3,0,7.9-5.49,8.17-9.55h1.55v8.86h6.93v2.19h-6.93v15.9c0,3.57,1.54,4.59,4.32,4.59a5.94,5.94,0,0,0,2-.32Z" fill="#fff"/><path d="M274.82,169.91h-1.31V169h3.72v.92h-1.32v3.92h-1.09Z" fill="#fff"/><path d="M281.87,172c0-.58,0-1.28,0-2h0c-.15.62-.35,1.31-.54,1.87l-.59,1.89h-.85l-.52-1.87c-.16-.57-.31-1.25-.44-1.89h0c0,.65-.05,1.4-.08,2l-.09,1.84h-1L278,169h1.46l.47,1.62c.16.56.3,1.16.41,1.73h0c.13-.56.29-1.2.46-1.74l.51-1.6h1.43l.26,4.83H282Z" fill="#fff"/></svg>
	</div>
</footer>
```
{% endtab %}
{% endtabs %}

1. In your editor open `/source/_patterns/04-pages/homepage.twig`

{% tabs %}
{% tab title="homepage.twig" %}
```php
{% include "@organisms/00-global/01-footer.twig" %}
```
{% endtab %}
{% endtabs %}

* If not already running run Pattern Lab and Gulp

```bash
npm start
```

```bash
npm run watch
```

