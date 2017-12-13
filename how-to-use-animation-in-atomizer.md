# How to use animation in atomizer? Can you give any example?

## Question from [@jitendravyas](https://github.com/jitendravyas) via [issue #1](https://github.com/thierryk/ACSS-QA/issues/1)

Let's try to reproduce this basic example from [The Guide To CSS Animation: Principles and Examples](https://www.smashingmagazine.com/2011/09/the-guide-to-css-animation-principles-and-examples/)

```css
/* This is the animation code. */
@-webkit-keyframes example {
   from { transform: scale(2.0); }
   to   { transform: scale(1.0); }
}

/* This is the element that we apply the animation to. */
div {
   -webkit-animation-name: example;
   -webkit-animation-duration: 1s;
   -webkit-animation-timing-function: ease; /* ease is the default */
   -webkit-animation-delay: 1s;             /* 0 is the default */
   -webkit-animation-iteration-count: 2;    /* 1 is the default */
   -webkit-animation-direction: alternate;  /* normal is the default */
}
```

To do so, one can choose to go *[shorthand](https://github.com/thierryk/ACSS-QA/new/master#shorthand)* or *[longhand](https://github.com/thierryk/ACSS-QA/new/master#longhand)*. Note that in both cases the animation needs to be part of a custom styles sheet or style block:

```css
@keyframes example {
   from { transform: scale(2.0); }
   to   { transform: scale(1.0); }
}
```

## Shorthand

This is just a matter of relying on the config file to pass all properties/values at once:

```js
"custom": {
    "example": "example 1s ease 1s 2 alternate",
    "foo": "bar"
}
```

and then using the class `Anim(example)` in the markup.

```html
<div class="Anim(example)">
    Example
</div>
```

## Longhand

In this case, we use each property with its appropriate value:

```html
<div class="Animn(exapmple) Animdur(1s) Animtf(e) Animdel(1s) Animic(20) Animdir(a)">
    Example
</div>
```

## Which one to choose?

You should choose the one that makes more sense to your use case.


