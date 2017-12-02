# [How would one style a component differently based on its neighbours while using Atomic CSS #11](https://github.com/jitendravyas/Q-A/issues/11)

## Question from [@chinchang](https://github.com/chinchang) 

Heres an example when using default class-based approach:

```html
<button class="btn">Hello</button>
```

When 2 buttons are required side-by-side as a group, we normally do:

```html
<div class="btn-group"
  <button class="btn">Hello</button>
  <button class="btn">Hello</button>
</div>
```

And in stylesheet we would have something like:

```css
// Removing border-radius of buttons to show they are visually grouped.
.btn-group > .btn:not(:first-child):not(:last-child) {
  border-radius: 0;
}
.btn-group > .btn:first-child {
  border-radius-top-right: 0;
  border-radius-bottom-right: 0;
}
.btn-group > .btn:last-child {
  border-radius-top-left: 0;
  border-radius-bottom-left: 0;
}
```

Now coming back to Atomic CSS, our Button component would be something like:

```html
<button class="Bgc(blue) Bdrs(4px) P(10px)">
```

To create above mentioned visual appearance of a button group, I could make a new Group component in which can wrap 2 buttons, like so:

```js
<Group>
  <Button>Hello</Button>
  <Button>World</Button>
</Group>
```

But the issue is that, since each component has its classes(styles) on itself, the Group component cannot affect the inner buttons in any way. One way I can think of is: Atomic CSS's contextual class. Using that approach the Group can add a class which the Button component can refer as a contextual class.

```html
<!-- Button -->
<button class="Bdrs(4px) Bdrs(0)__group">
```

Is this the best way to achieve my requirement?

## Answer

Using [ACSS](https://acss.io) we can rely on the `>` combinator and pseudo-classes to contextually style these buttons. 

In the config:

```js
"custom": {
  "Bdrs-start": "4px 0 0 4px",
  "Bdrs-end": "0 4px 4px 0"
}
```

In the markup:

```html
<div class="group">
    <button class="Bgc(blue) P(10px) Bdrs(4px) group>Bdrs(0) group>Bdrs(Bdrs-start):fc group>Bdrs(Bdrs-end):lc">button</button>
    <button class="Bgc(blue) P(10px) Bdrs(4px) group>Bdrs(0) group>Bdrs(Bdrs-start):fc group>Bdrs(Bdrs-end):lc">button</button>
    <button class="Bgc(blue) P(10px) Bdrs(4px) group>Bdrs(0) group>Bdrs(Bdrs-start):fc group>Bdrs(Bdrs-end):lc">button</button>
</div>
```

This way we can apply the **exact same classes to all** our `<Button>` instances&mdash;**regardless of context**:

   * if a button has no siblings, all its corners will be rounded; 
   * if it is in-between siblings, none of its corners will be rounded; 
   * if it is the first child of a group of buttons, only its left corners will be rounded;
   * if it is the last child of a group, then only its right corners will be rounded.

**Important note**: as I strongly suggest in [my article on Smashing Magazine](https://www.smashingmagazine.com/2013/10/challenging-css-best-practices-atomic-approach/), adopting Atomic CSS methodology does not mean to "Atomic CSS all the things!". The idea is to know how to do any kind of styling and then decide which approach makes more sense, and that mostly depends on the project at hand. In the above example, even though these classes will compress very well (since they are all *duplicates*.) it may, or may not, be wiser to go the classic route. It's up to the author to make that decision.

