# [Why Atomizer (acss.io) didn't use more readable class names? #5](https://github.com/jitendravyas/Q-A/issues/5)

## Question from [@jitendravyas](https://github.com/jitendravyas)

or [Atomic classes looks ugly, why do yahoo use it?](https://github.com/jitendravyas/Q-A/issues/2)

## Answer

These were more or less the features/benefits we wanted to *gain* from the [ACSS](htps://acss.io) syntax:

   * It needed to facilitate parsing so we could make many things possible, like:
      * declaring any unit and/or value,
      * using combinators for contextual styling, 
      * using pseudo-classes and pseudo-elements,
      * using media queries, 
      * using RTL/LTR-agnostic classes,
      * and more...
   * It needed to produce short strings which:
      * are **faster to type** (this was very important to us since using Atomic CSS means writing many, many, many classes),
      * create **less bytes** in Styles Sheets *and* markup
   * It needed to help devs "guess" what style was associated with each class (the reason why we used something similar to [Emmet](https://docs.emmet.io/cheat-sheet/) abbreviations)

## Dynamic libraries are a whole different ball game

It is much more complex to create classes meant to be parsed by a tool (see dynamic libraries like [ACSS](http://acss.io) or [Blowdrycss](http://blowdrycss.readthedocs.io/en/latest/syntax.html)) than classes for static libraries. This is because tools used by dynamic libraries must rely on specific *patterns* to help express rich styles (contextual styling, media queries, pseudo-classes, etc.) through syntax alone. Static libraries do not have such *constraints*.

## What does *readable* mean anyway?

Let's take a look at various syntaxes for the sake of comparison:

Declarations | Tailwind CSS | Blowdrycss| Basscss | Tachyons | ACSS
-- | -- | -- | -- | -- | --
**`margin: 1rem`** | `.m-4` | `.margin-1rem` | `.m2` | `.ma3` | `.M(1rem)`
**`text-align: center`** | `.text-center` | `.text-align-center` | `.center` | `.tc` | `.Ta(c)`
**`font-weight: 900`** | `.font-black` | `.font-weight-900` | - | `.fw9` | `.Fw(900)`
**`width: 100vw`** | `.w-screen` | `.width-100vw` | - | - | `.W(100vw)`

I may be a bit biased, but it seems to me that the ACSS and Blowdrycss classes better associate with their corresponding style (**`property: value`**). In that sense, those classes seem to be more "readable".

Notes:
   * Blowdrycss offers aliases that work as abbreviations (i.e. `.fw-900`).
   * Basscss does not have a class for `font-weight: 900` it only has a `.bold`class.

### When "not readable" is actually **more readable**

Let's consider negative values, units, percentage, and decimal points:

Declarations | Tailwind CSS | Blowdrycss| Basscss | Tachyons | ACSS
-- | -- | -- | -- | -- | --
**`margin: -1rem`** | `.-m-4` | `.margin-n1rem` | `.mxn2` | `.na3` | `.M(-1rem)`
**`font-size: 25px`** | `.text-2xl` | `.font-size-25` | `.h2` | `.f3` | `.Fz(25px)` 
**`width: 50%`** | `.w-1/2` | `.width-50p` | `.col-6` | `.w-50` | `.W(50%)`
**`line-height: 1.5`** | `.leading-normal` | `.line-height-1_5` | `.line-height-4` | `.lh-copy` | `.Lh(1.5)`

With ACSS, we use `-` for minus, we use *explicit* units (i.e. `px`), we use `%` for percentage, and we even use `.` for decimal point. How *crazy* is that?

Note:
   * the "abstraction" offered by static libraries has no relevance here since Atomizer (and Blowdrycss?) can do that as well (i.e. `.Fz(2xl)`).
   * "basscss" does not have a class for negative margin on all sides , so I'm showing their class for negative left/right margins. 
   * "blowdrycss" uses `p` for "percentage" so I'm not sure what one needs to use for `point`.

## Readable versus Guessable

*Readable* is **not the same** as *guessable*. For example, it may be easy for one to understand what [`.uppercase`](https://github.com/tailwindcss/tailwindcss/blob/master/dist/utilities.css) does, or even what [`.lowercase`](https://github.com/tailwindcss/tailwindcss/blob/master/dist/utilities.css) does, but do these names help you guess *which class should be used* for `text-transform: none`? 
Anyone? Anyone?

In my opinion, helping devs figure things out by themselves is a better approach because they only need to learn a [**mnemonic pattern**](https://acss.io/guides/syntax.html#the-syntax) rather than a new **vocabulary**. In other words, I think it's better to have a tool (i.e. a strict "[syntax](https://acss.io/guides/syntax.html#the-syntax)") to be able to mentally construct classes by oneself (ACSS/Blowdrycss) than to have to learn a slew of **arbitrary** names (i.e. `.float-right`, `.right`, `.fr`, etc.).

## Did you guess?

I asked above what should be the class to be used for `text-transform: none` in the context of classes like `.uppercase` and `lowercase`. Let's see the syntax for that across the same few libraries:

Declarations | Tailwind CSS | Blowdrycss| Basscss | Tachyons | ACSS
-- | -- | -- | -- | -- | --
**`text-transform: uppercase`** | `.uppercase` | `.text-transform-uppercase` | `.caps` | `.ttu` | `.Tt(u)`
**`text-transform: lowercase`** | `.lowercase` | `.text-transform-lowercase` | - | `.ttl` | `.Tt(l)` 
**`text-transform: none`** | `.normal-case` | `.text-transform-none` | - | `.ttn` | `.Tt(n)`

I think it is correct to assume that even though the classes `.uppercase` and `.lowercase` are the most "readable" (in the general sense), they are also the ones that do not help devs *predict* which class they should use for `text-transform: none`. This is why I think it is important that the naming convention/syntax helps people use a class without the need to learn about it first.

Note: 
   * "Blowdrycss" also offers `.uppercase` and `.lowercase` aliases. 
   * "Basscss"'s `.caps` adds `letter-spacing` too.  

---

**And there is this:**

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Without knowing anything about atomiccss i was able to grok exactly what each class meant. Neat.</p>&mdash; Ryan Seddon (@ryanseddon) <a href="https://twitter.com/ryanseddon/status/936733186758926336?ref_src=twsrc%5Etfw">December 1, 2017</a></blockquote>

