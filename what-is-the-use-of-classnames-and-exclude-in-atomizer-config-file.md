# [What is the use of 'classNames': [] and 'exclude': [] in Atomizer's config file? #7](https://github.com/jitendravyas/Q-A/issues/7)

## Question from [@jitendravyas](https://github.com/jitendravyas)

Can you please explain with an example? I didn't get it by reading comment [from here](https://github.com/acss-io/atomizer/blob/496469f94a690cdedcd77691a3d977a3576f011c/examples/example-config.js):

```js
module.exports = {
  'custom': {
    uh: '79px',         // custom 1 (see classNames below)
    primary: '#f6a1e1'  // custom 2 (see classNames below)
  },
  'classNames': [
    'H(uh)',            // custom 1 (maps to 'custom' key above)
    'C(primary)',       // custom 2 (maps to 'custom' key above)
    'Td(u)',            // normal
    'Td(u):h',          // pseudo classs
    'Bgc(#333)',        // hex value
    'Bgc(#fff.8)'       // hex value + alpha
  ],
  'exclude': [
    'Fl(end)'
  ]
};
```

## Answer

Here is a simple example that explains the use of both `classNames` and `exclude` in the config file. 

Open [Atomizer-Web](https://pankajparashar.com/atomizer-web/) and do this:

   1. Replace the content of the config with this:
(click on the &#9881;&nbsp;  icon to access the configuration panel)

```js
{
  "custom": {
    "l": "left",
    "r": "right"    
  },
  "classNames": [
    "Fl(l)",
    "Fl(r)"
  ],
  "exclude": [
    "Fl(start)",
    "Fl(end)"
  ]
}
```

   2. Replace the existing markup in the tool with this:

```html
<div class="Fl(start)">
  Left
</div>
<div class="Fl(end)">
  Right
</div>
```

   3. The panel in which the CSS is generated should show this:

```css
.Fl\(l\) {
  float: left;
}
.Fl\(r\) {
  float: right;
}
```

In the example above, we are "*replacing*" the keywords `start` and `end` that ACSS uses to be RTL/LTR-agnostic by the more "familiar" `l` and `r` abbreviations. 

As the CSS panel shows, authors can no longer use `Fl(start)` nor `Fl(end)` as those classes are **ignored** by Atomizer (thanks to `exclude`). On the other hand, they can now use `Fl(l)` and `Fl(r)` in lieu of the RTL-LTR-friendly classes (thanks to `classNames`,  and `custom`).

In other words, `classNames` will make Atomizer generate classes even if they are not present in the files it parses; while `exclude` will prevent Atomizer from generating classes *even* if they are found in files throughout a project. 

---

Another reason why one would want to use `classNames` is if they have ACSS classes "*constructed*" via JS, for example:

```js
"Fl(" + direction + ")"
```
 
They'd need to add both `Fl(start)` and `Fl(end)` in the config as Atomizer would not find those classes while parsing that JS file.
