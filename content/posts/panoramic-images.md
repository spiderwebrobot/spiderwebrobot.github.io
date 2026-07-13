+++
date = '2026-07-08T07:57:28-07:00'
draft = false
title = 'Panoramic images'
summary = 'Moving pictures.'
+++

Hey team, let’s position an oversized image inside of a viewport with CSS [translate](https://developer.mozilla.org/en-US/docs/Web/CSS/transform-function/translate). Check out this [proof of concept](https://codepen.io/spiderwebrobot/live/ogzJxZK) as we dig into the details.

## The building blocks

The solution requires 3 [HTML](https://developer.mozilla.org/en-US/docs/Learn/HTML/Introduction_to_HTML/Getting_started) elements.

```html
<div class="pan">
  <div class="pan-x">
    <img class="pan-y" src="https://dw9to29mmj727.cloudfront.net/promo/2016/5945-SeriesHeaders_DemonSlayer_2000x800_wm.jpg" height="800" width="2000" alt="Tanjiro and Nezuko" />
  </div>
</div>
```

A **pan** element that hides the image overflow, and sets the viewport’s height. A **pan-x** element that moves the image along the X axis, and a **pan-y** element that moves the image along the Y axis.

```css
.pan {
  height: 450px;
  overflow: hidden;
}
.pan-x,
.pan-y {
  transition-property: transform;
  transition-duration: 3.6s;
  transition-timing-function: ease-in-out;
}
```

## Starting positions

```css
.pan-x.start {
  transform: translateX(0);
}
.pan-y.start {
  transform: translateY(0);
}
```

🎃
{.pan .northwest}

The **northwest** corner of the image is visible by default. All X and Y movements **start** from these positions.
{.float-right}

## Moving along the X axis
{.clear-float}

### The northeast corner

```css
.pan-x.end {
  transform: translateX(100%) translateX(-2000px);
}
```

🎃
{.pan .northeast}

The **northeast** corner of the image is revealed in 2 movements. Starting from the northwest corner, the image is pushed right, completely out of view (100%). Next, the image is pulled left, back into view (-2000px), until it’s **flush right** inside of the viewport.
{.float-right}

### North of center
{.clear-float}

```css
.pan-x.center {
  transform: translateX(50%) translateX(-1000px);
}
```

🎃
{.pan .north}

The **north** side of the image is revealed in 2 movements. Starting from the northwest corner, the image is pushed right, halfway out of view (50%). Next, the image is pulled left, halfway into view (-1000px), until it’s **centered horizontally** inside of the viewport.
{.float-right}

## Moving along the Y axis
{.clear-float}

### The southwest corner

```css
.pan-y.end {
  transform: translateY(-100%) translateY(450px);
}
```
🎃
{.pan .southwest}

The **southwest** corner of the image is revealed in 2 movements. Starting from the northwest corner, the image is pulled up, completely out of view (-100%). Next, the image is pushed down, back into view (450px), until it’s **flush bottom** inside of the viewport.
{.float-right}

### West of center
{.clear-float}

```css
.pan-y.center {
  transform: translateY(-50%) translateY(225px);
}
```
🎃
{.pan .west}

The **west** side of the image is revealed in 2 movements. Starting from the northwest corner, the image is pulled up, halfway out of view (-50%). Next, the image is pushed down, halfway into view (225px), until it’s **centered vertically** inside of the viewport.
{.float-right}

## Moving along the X/Y axes
{.clear-float}

### The southeast corner

```html
<div class="pan">
  <div class="pan-x end">
    <img class="pan-y end" src="https://dw9to29mmj727.cloudfront.net/promo/2016/5945-SeriesHeaders_DemonSlayer_2000x800_wm.jpg" height="800" width="2000" alt="Tanjiro and Nezuko" />
  </div>
</div>
```

🎃
{.pan .southeast}

The **southeast** corner of the image is revealed by moving the image to the **end** along the X and Y axes.
{.float-right}

### East of center
{.clear-float}

```html
<div class="pan">
  <div class="pan-x end">
    <img class="pan-y center" src="https://dw9to29mmj727.cloudfront.net/promo/2016/5945-SeriesHeaders_DemonSlayer_2000x800_wm.jpg" height="800" width="2000" alt="Tanjiro and Nezuko" />
  </div>
</div>
```

🎃
{.pan .east}

The **east** side of the image is revealed by moving the image to the **end** along the X axis, and to the  **center** along the Y axis.
{.float-right}

### South of center
{.clear-float}

```html
<div class="pan">
  <div class="pan-x center">
    <img class="pan-y end" src="https://dw9to29mmj727.cloudfront.net/promo/2016/5945-SeriesHeaders_DemonSlayer_2000x800_wm.jpg" height="800" width="2000" alt="Tanjiro and Nezuko" />
  </div>
</div>
```

🎃
{.pan .south}

The **south** side of the image is revealed by moving the image to the **center** along the X axis, and to the **end** along the Y axis.
{.float-right}

### Centering the image
{.clear-float}

```html
<div class="pan">
  <div class="pan-x center">
    <img class="pan-y center" src="https://dw9to29mmj727.cloudfront.net/promo/2016/5945-SeriesHeaders_DemonSlayer_2000x800_wm.jpg" height="800" width="2000" alt="Tanjiro and Nezuko" />
  </div>
</div>
```

🎃
{.pan .center}

The **center** of the image is revealed by moving the image to the **center** along the X and Y axes.
{.float-right}

## The push and pull
{.clear-float}

Moving an oversized image inside of a viewport is a 2-step process. Check out this [prototype](https://codepen.io/spiderwebrobot/live/emBNNNe) as we break them down.

### Pushing/pulling along the X axis

1. **Push** the image out of view a percentage of the viewport’s width
2. **Pull** the image into view a fraction of the image’s (negative) width

```css
:root {
  --x: 0.5;
  --x-offset: -2000px;
}
.pan-x {
  transform: translateX(calc(var(--x) * 100%))
    translateX(calc(var(--x) * var(--x-offset)));
}
```

### Pulling/pushing along the Y axis

1. **Pull** the image out of view a percentage of the image’s height
2. **Push** the image into view a fraction of the viewport’s height

```css
:root {
  --y: 0.5;
  --y-offset: 450px;
}
.pan-y {
  transform: translateY(calc(var(--y) * -100%))
    translateY(calc(var(--y) * var(--y-offset)));
}
```

## Transitioning to animations

So far we’ve used CSS [transitions](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_transitions/Using_CSS_transitions) to move images, but what if we wanted to use CSS [animations](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_animations/Using_CSS_animations)? Check out this [attempt](https://codepen.io/spiderwebrobot/live/jEVxPOL) as we do some refactoring.

### Configuring the animations

Let’s start by configuring the shared animation properties...

```css
:root {
  --duration: 7.2s;
}
.pan-x,
.pan-y {
  animation-direction: normal;
  animation-duration: var(--duration);
  animation-fill-mode: forwards;
  animation-iteration-count: 1;
}
```

### Animate X

Next we’ll configure the X axis animation and sequence it...

```css
:root {
  --x: 0.56;
  --x-offset: -2000px;
  --x-timing-function: ease-in-out;
  --x-tween: 0.45;
}
.pan-x {
  animation-name: animate-x;
  animation-timing-function: var(--x-timing-function);
}
@keyframes animate-x {
  0% {
    transform: translateX(calc(var(--x) * 100%))
      translateX(calc(var(--x) * var(--x-offset)));
  }
  45% {
    transform: translateX(calc(var(--x-tween) * 100%))
      translateX(calc(var(--x-tween) * var(--x-offset)));
  }
  100% {
    transform: translateX(calc(var(--x) * 100%))
      translateX(calc(var(--x) * var(--x-offset)));
  }
}
```

### Animate Y

Finally we’ll configure the Y axis animation and sequence it...

```css
:root {
  --y: 0.36;
  --y-offset: 450px;
  --y-timing-function: linear;
  --y-tween: 0.63;
}
.pan-y {
  animation-name: animate-y;
  animation-timing-function: var(--y-timing-function);
}
@keyframes animate-y {
  0% {
    transform: translateY(calc(var(--y) * -100%))
      translateY(calc(var(--y) * var(--y-offset)));
  }
  54% {
    transform: translateY(calc(var(--y-tween) * -100%))
      translateY(calc(var(--y-tween) * var(--y-offset)));
  }
  100% {
    transform: translateY(calc(var(--y) * -100%))
      translateY(calc(var(--y) * var(--y-offset)));
  }
}
```


## Considerations

- The **image** should be **larger than** its **viewport**. The more an image is hidden, the greater its range of motion.
- The [img](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/img) element can be replaced by a [picture](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/picture) element for **art direction**.
- Animations should last **5 seconds** or **less**, otherwise they may require [controls](https://www.w3.org/WAI/WCAG21/Understanding/pause-stop-hide.html) to play and pause them.
- Some folks prefer [reduced motion](https://www.joshwcomeau.com/react/prefers-reduced-motion/).

## Use the fork

We’re better together. Please fork the following CodePens to share your innovations with the rest of the team. 

- [Panoramic directions](https://codepen.io/spiderwebrobot/pen/ogzJxZK)
- [Panoramic coordinates](https://codepen.io/spiderwebrobot/pen/emBNNNe)
- [Panimation](https://codepen.io/spiderwebrobot/pen/jEVxPOL)

## Resources

- [transform CSS property](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/transform)
- [Why Moving Elements With Translate() Is Better Than Pos:abs Top/left](https://www.paulirish.com/2012/why-moving-elements-with-translate-is-better-than-posabs-topleft/)
- [How to Create Curved CSS Animation Path](https://redstapler.co/curved-css-animation-path/)
