# [Why are Atomizer classes capitalized? #9](https://github.com/jitendravyas/Q-A/issues/9)

## Question from [@jitendravyas](https://github.com/jitendravyas)

```html
<div class="D(f) Jc(c) Ai(c) H(100%) Fz(20vh) Ff(m)">
  Preview
</div>
```

## Answer

From the [FAQ page]():

> Q: **Why are Atomic classes capitalized? As far as I know, no other framework does that?**
>
> A: We took advantage of the fact that nobody seems to capitalize classes and that CSS is case sensitive to get a "cheap" namespace, one that does not rely on an extra character(s).

---

From our "acss-io/atomizer" Gitter chat:

> Before using [ACSS](https://acss.io) at Yahoo! we used a *static* Atomic CSS library. At the time, we chose to use the capital letter as a mean to prevent styles collision (classes are case sensitive in CSS). Our logic was that even if somebody was using the same classes than ours they would not start them with a capital letter. 

I think we then kept that distinction to be consistent with our *helper* classes for which there was more risk of styles collisions (eg. I'm sure we're not the only ones to use the abbreviation "cf" for "clearfix" or even "row" for layout, etc.). The use of the capital letter makes sure `.Cf` and `.cf` do not collide. For ACSS classes we were less concerned because nobody used *parenthesis* in classes at the time (even though I see people starting to use that now). So if I recall it was mostly to be consistent across the board (Atomizer classes *and* ACSS helpers).

Personally, the "look" does not bother me at all because the capital letter stands out and helps me identify quickly the property associated with it. When it's all lowercase I have a problem with "i", "l" (eg. "`Lh(n)`" versus "`lh(n)`"), and other letters depending on the letter that follows (in my opinion it's **cognitively** better). The problem to me is more related to the fact that it requires authors to use an extra key (the `<shift>` key) :-(
