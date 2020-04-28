# JSON Basics

### What is JSON?

JavaScript Object Notation \(JSON\) is a standard text-based format for representing structured data based on JavaScript object syntax. It is commonly used for transmitting data in web applications \(e.g., sending some data from the server to the client, so it can be displayed on a web page, or vice versa\). You'll come across it quite often, in fact, Pattern Lab uses JSON to simulate the data structure of components.

JSON uses a `key` \| `value` pair format that makes writing and reading JSON a relatively easy task. You can include the same basic data types inside JSON as you can in a standard JavaScript object — strings, numbers, arrays, boolean, and other object literals. This allows you to construct a data hierarchy, like so:

```yaml
{
  "name": "John Smith",
  "email": "jsmith@example.com"
  "active": true,
  "social_networks": [
    {
      "name": "facebook",
      "url": "http://facebook.com"
    },
    {
      "name": "twitter",
      "url": "http://twitter.com"
    }
  ]
}
```

* The code above shows how each key to the left of the colon, has a value to the right of the colon.
* It also shows the different types of data we can store.  For example, `"name"` is a string type of data where you can enter any string of text and numbers.  `"active"` only accepts `true` or `false` as it is a boolen type of data field.  Finally we see that `"social_networks"` is an array which contains a collection of items within it.  Arrays can be visually identified by the square brackets, `[ ]` that wrap the items within it.

### What role does JSON play in Pattern Lab?

If you are a designer or developer chances are you have used tools like **Lorem Ipsum** to create "dummy" content for a webpage you may be designing or developing.  This helps build prototype-like assets that simulate how a given page or component will look when content is added to it.  Think of JSON, in the context of building components in Pattern Lab, as the tool that lets you generate the Lorem Ipsum dummy content.  So If I need a title or an image for my component, I can create a JSON file and add those fields I need for the component. There is a lot more you can do with JSON, but in the context of this training, JSON is only used to provide stock or dummy content to the things we build in Pattern Lab

{% hint style="info" %}
Read [more about JSON](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/JSON) to become more familiar with it.
{% endhint %}

