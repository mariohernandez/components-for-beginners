# Sass Basics

**Sass** (short for syntactically awesome style sheets) is a style sheet language initially designed by Hampton Catlin and developed by Natalie Weizenbaum.

Sass is a preprocessor scripting language that is interpreted or compiled into Cascading Style Sheets (CSS). Sass consists of two syntaxes. The original syntax, called "the indented syntax," uses a syntax similar to Haml.[4] It uses indentation to separate code blocks and newline characters to separate rules. The newer syntax, "SCSS" (Sassy CSS), uses block formatting like that of CSS. It uses braces to denote code blocks and semicolons to separate rules within a block. The indented syntax and SCSS files are traditionally given the extensions .sass and .scss, respectively.

All Sass/SCSS code compiles back to standard CSS so the browser can actually understand and render the results. Browsers currently don’t have direct support for Sass/SCSS or any other CSS pre-processor, nor does the standard CSS specification provide alternatives for similar features (yet.)

Sass and SCSS will refer to roughly the same thing. Conceptually, there isn’t much difference. You will learn the difference as you learn more, but basically SCSS is the one most people use now. It’s just a more recent (and according to some, superior) version of the original Sass syntax.

## What can Sass do that Vanilla CSS can’t?
1. **Nested Rules**: Nest your CSS properties within multiple sets of {} brackets. This makes your CSS code a bit more clean-looking and more intuitive.
2. **Variables**: Standard CSS has variable definitions. So what’s the deal? You can do a lot more with Sass variables: iterate them via a for-loop and generate property values dynamically. You can embed them into CSS property names themselves. It’s useful for property-name-N { … } definitions.
3. **Better Operators**: You can add, subtract, multiply and divide CSS values. Sure the original CSS implements this via calc() but in Sass you don’t have to use calc() and the implementation is slightly more intuitive.
4. **Functions**: Sass lets you create CSS definitions as reusable functions. Speaking of which…
5. **Trigonometry**: Among many of its basic features (+, -, *, /), SCSS allows you to write your own functions. You can write your own sine and cosine (trigonometry) functions entirely using just the Sass/SCSS syntax just like you would in other languages such as JavaScript. Some trigonometry knowledge will be required. But basically, think of sine and cosine as mathematical values that help us calculate the motion of circular progress bars or create animated wave effects, for example.
6. **Code Flow and Control Statements**: You can write CSS using familiar code-flow and control statements such as for-loops, while-loops, if-else statements similar to another languages. But don’t be fooled, Sass still results in standard CSS in the end. It only controls how property and values are generated. It’s not a real-time language. Only a pre-processor.
7. **Mixins**. Create a set of CSS properties once and reuse them or “mix” together with any new definitions. In practice, you can use mixins to create separate themes for the same layout, for example.

## Sass Pre-Processor
Sass is not dynamic. You won’t be able to generate or animate CSS properties and values in real-time. But you can generate them in a more efficient way and let standard properties (CSS animation for example) pick up from there.

## New Syntax
SCSS doesn’t really add any new features to the CSS language. Just new syntax that can in many cases shorten the amount of time spent writing CSS code.
