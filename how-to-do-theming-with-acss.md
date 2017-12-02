# How to do "theming" with ACSS?

## Question from [@jitendravyas](https://github.com/jitendravyas) via Gitter

Atomizer config is not able to do this:

```js
{
  "custom": {
    "Color-red": "#FF0000",
    "Danger": "Color-red"
  }
}
```

I think real time themeable website is not possible with Atomizer.

## Answer

For theming, it is best to leverage *custom properties* (aka CSS variables) and that's **really easy to do with Atomizer**.

In the config:

```js
{
  "custom": {
    "primaryColor": "var(--primaryColor)",
    "secondaryColor": "var(--secondaryColor)"
  }
}
```

In the markup:

```html
<div class="C(primaryColor) Bgc(secondaryColor)">...</div>
```

In a CSS file or `<style>` block we set default values:

```css
:root {
  --primaryColor: teal;
  --secondaryColor: indianred;  
}
```

We can then use JavaScript to apply new values:

```html
<body style="--primaryColor:aliceblue;--secondaryColor:bisque;">
```

Et voilà!

In short, the idea is to **not set hard-coded color values** through ACSS, but rather relying on (CSS) variables alone.
