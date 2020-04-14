# Exercise 2.1

Probably the first thing you should look at to determine if a component is a candidate for variants, is the data fields, and second, the component's markup.

Visually we know the two different variants look similar, however, if we pay close attention we will notice that the data fields between the variants are different. In this particular case although some of the fields may be different, I feel we have enough of shared attributes between the variants that we should have no problem going the variant route vs. new components. Let's start! The new variant will be called **Card wide**.

![Card wide variant](../.gitbook/assets/card-wide.png)

We can see that the overall layout of the "Card wide" lends itself nicely to a variant. However, we see that some of the fields found in the original card are not present here \(tags\), and, there is also a new field in this variant that is not part of the original card \(button\).

Before we can create a new variant, we need to make some updates to the original Card component so it is easier to adapt it to new variant.

