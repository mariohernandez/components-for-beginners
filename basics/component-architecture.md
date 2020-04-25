# Component Architecture

I typically recommend to group components or patterns in individual folders. This not only provides organization as your catalog of components grows, but it also makes each component completely reusable and even portable as all the pieces of a component are encapsulated in a single folder. Here's a typical architecture of a component. Your particular workflow may vary.

```text
+
|--source
|  |--_patterns
|     |--00-molecules
|        |--card
|           |-- card.js
|           |-- card.md
|           |-- card.scss
|           |-- card.twig
|           |-- card.json
+
```

A component is typically broken down in four parts:

* **Markup**: Markup or HTML for a component is written in Twig templates, a PHP templating engine. The naming convention for a component twig template looks like this: **card.twig** \(where card is the name of the component\).
* **Data**: Dummy or stock data for components is usually provided in YAML or JSON format. These are lightweight formats for storing data. In this training we will use JSON \(**J**ava**S**cript **O**bject **N**otation\).
* **Styles**: These are written in CSS or SCSS.
* **Behavior/interaction**: The component's behaviors are usually handled with JavaScript.  Most components don't need JavaScript.
* **Annotations** \(Optional\): Annotations are used to document the details of a component and are typically written in markdown format \(`.md`\). This is extremely useful for teams because it outlines technical details of a pattern such as variable names, attributes, data structure, etc.



