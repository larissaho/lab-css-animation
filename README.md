# Lab: CSS Animations

In this short lab you will be exploring how to perform basic animations with CSS.

### Resources
- [MDN: Using CSS Transitions](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Transitions/Using_CSS_transitions)
- [MDN: Using CSS Animations](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Animations/Using_CSS_animations)

### Set up
The initial page for this lab shows a number of "boxes" on the screen, each of which is implemented as a `<div>` with the class `box`. Your task will be to add rules to the **`css/style.css`** file to make these boxes animated! Instructions are listed below. They assume you will _read the documentation_ listed above for specific details on syntax and options&mdash;practice learning on your own!

Note that you can easily write a rule that applies to a single box by using the `nth-of-type` pseudo-selector. For example, to select just the first box, you could use `.box:nth-of-type(1)`.


## Transitions
The simplest way to add an animation is to specify a **transition** using the [**`transition`**](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Transitions/Using_CSS_transitions) property. This property specifies that when some _other_ property is changed, that should occur over time rather than immediately. Transitions are intended to be used with rules that are applied after the page loads&mdash;for example, a `:hover` rule that will only apply when the element is hovered, or when a new class is added to an element via JavaScript.

```css
/* The initial "starting" properties */
#element {
  font-size: 16px;
  transition: font-size 2s; /* change over time */
}

/* The "target" properties when hovering */
#element:hover {
  font-size: 20px;
}
```

With the above rules, instead of having the `font-size` _immediately_ go to `20px` when you hover, the `transition` property indicates that the property should instead move towards that size over a lenth of 2 seconds. The property value will be _interpolated_, so after half the time (1 second) it will be halfway to the new size (i.e., `18px`). Note that properties that are not listed as `transition` options will up updated immediately.

**Task 1:** Add a CSS rule so that when you hover over Box 1, it gains a `border-radius` property with a value of `50px`. Have this transition occur over `.5s`

**Task 2** Add a CSS rule so that when you hover over Box 2, it "explodes"&mdash;it's size should [scale](https://www.w3schools.com/cssref/css3_pr_transform.asp) to 10x its size over 2 seconds, and its `opacity` should drop to 0 over 3 seconds. Bonus: add a [_timing function_](https://developer.mozilla.org/en-US/docs/Web/CSS/transition-timing-function) so that the box expands quickly but then slows down over time.

## Animations
While it is possible to use delays and multiple properties to produce "multi-step" transitions (see [here](https://css-tricks.com/using-multi-step-animations-transitions/) for one set of examples), it's often easier to specify a complex **animation** using the [**`animation`**](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Animations/Using_CSS_animations) property. They property allows you to specify a set of "key frames" (e.g., "stop points") that the element should have at different points during the animation; the element will then automatically interpolate between all of these frames.

You specify keyframes by using an `@keyframes` rule, followed by a label/name for the keyframe-set, followed by a block of properties and at what percentage through the animation they should be shown:

```css
/* example adapted from w3schools */

/* define a set of keyframes called `slidein` */
@keyframes bounce {
  /* properties at 0% of animation duration (start; can write as `from`) */
  0% {
    top: 0px; /* start 0px down */
  }
  /* properties at 50% of animation duration */
  50% {
    top: 200px; /* drop to 200px down */
  }
  /* properties at 100% of animation duration (end; can write as `to`) */
  100% {
    top: 0px /* go back to 0px down */
  }
}
```

You can then have an element perform this animation by using the `animation` property, and specifying the name of the keyframe set. You can also specify the duration of the animation (the usual second value), as well as other customizations:

```css
#element {
  position: relative;
  animation: bounce 5s; /* run bounce animation over 5 seconds */
}
```

**Task 3** Add a CSS rule specifying a keyframe set called `rainbow`. This keyframe should start the `background-color` at `red`, and then change it to `orange`, `yellow`, `green`, `blue`, and `indigo`, in that order. You can spread them throughout the duration however you wish. Then add a rule so that Box 3 cycles through this animation over a 10 seconds duration (constantly, not just when you hover). Add animation options so that the animation is in an `infinite` loop, repeating in an `alternate` direction each time.

**Task 4** Add a CSS rule so that when you hover over Box 4, it "zooms" around the page in some way! you can use an animation or a multi-step transition.

Bonus: try searching around for CSS animation examples. What other cool effects can you find demos for (or think of on your own)?
