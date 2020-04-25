# JSON Basics

JavaScript Object Notation \(JSON\) is a standard text-based format for representing structured data based on JavaScript object syntax. It is commonly used for transmitting data in web applications \(e.g., sending some data from the server to the client, so it can be displayed on a web page, or vice versa\). You'll come across it quite often, in fact, Pattern Lab uses JSON to simulate the data structure of components.

JSON uses a `key` \| `value` pair format that makes writing and reading JSON relatively easy task. You can include the same basic data types inside JSON as you can in a standard JavaScript object — strings, numbers, arrays, booleans, and other object literals. This allows you to construct a data hierarchy, like so:

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

{% hint style="info" %}
Read [more about JSON](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/JSON) to become more familiar with it.
{% endhint %}

