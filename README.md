# Utopia PostCSS Demo

A demonstration of fluid typography using the Utopia PostCSS plugin.

## About Utopia

Utopia provides a fluid type scale that smoothly transitions between different viewport sizes. The PostCSS plugin makes it easy to implement Utopia's fluid type scale in your CSS.

For more information, visit [Utopia's website](https://utopia.fyi/).

## Project Structure

- `typography.css` - Contains the Utopia type scale configuration
- `index.css` - Main CSS file that imports typography and defines layout
- `index.html` - The demo page showing different type sizes
- `postcss.config.js` - PostCSS configuration with the Utopia plugin
- `server.js` - Simple Express server to serve the demo

## Setup

1. Install Utopia PostCSS

```shell
pnpm install postcss-utopia
# or
npm install postcss-utopia
```

2. Install dependencies:

```bash
npm install
# or
pnpm install
```

3. Build the CSS files:

```bash
npm run build:css
# or
pnpm build:css
```

4. Start the server:

```bash
npm start
# or
pnpm start
```

5. Open your browser and navigate to http://localhost:3000

:tada:

## Development

To watch for CSS changes and rebuild automatically:

```bash
npm run watch:css
# or
pnpm watch:css
```

:bulb:

### Questions :question:

1.

In the referenced documentation https://github.com/trys/postcss-utopia?tab=readme-ov-file#utopia-typescale the typescale has the object syntax.

```css
:root {
  @utopia spaceScale({
    minWidth: 320,             /* Defaults to plugin minWidth */
    maxWidth: 1240,            /* Defaults to plugin maxWidth */
    minSize: 16,
    maxSize: 18,
    positiveSteps: [1.5, 2, 3],
    negativeSteps: [0.75, 0.5],
    customSizes: ['s-l'],
    relativeTo: 'viewport',    /* Optional */
    prefix: 'space',           /* Optional */
    usePx: false,              /* Optional */
  });

  /* Generates
  --space-2xs: clamp(...);
  --space-xs: clamp(...); etc.

  --space-2xs-xs: clamp(...); etc.

  --space-s-l: clamp(...); etc.
  */
}
```

This leads to the following :boom: error in the <a href="/typography.css">typography.css</a> file that is responsible for defining the type steps.

<img src="/docs/data/001-Screenshot_20250505_155125.png">

How do the author's of the PostCSS Plugin handle this error, it is possible to get rid of the error and if so how ?

2.

Given this article https://utopia.fyi/blog/designing-with-fluid-type-scales I understand that instead of having multiple type scales, one for small screens and one for large screens, we can tell the browser to interpolate between these two type scales to obtain a set of type sizes which are always “in tune” with themselves and feel at home on any device.

So far so good.

But what can one do when indeed 2 or more "in tune" and interpolated type scales are desired throughout the design ?

https://www.smashingmagazine.com/2022/01/modern-fluid-typography-css-clamp/#using-negative-viewport-value-for-fluid-sizing

Or better, what can we do to achieve a reversing type scale at first, for small to medium screens that interpolate into an increasing type scale for medium to large screens later on ?

<img src="docs/data/10-modern-fluid-typography-css-clamp.gif">

I understand that that would lead to literally having a breakpoint point `breakpoint` in the design that would be the border of where the decreasing type scale ends and the increasing type scale begins, right ?

So to confirm, it is always either increasing or decreasing, correct ?

Here is an example of a decreasing type scale.

```css
:root {
  @utopia typeScale({
    minWidth: 320,
    maxWidth: 1240,
    minFontSize: 28,
    maxFontSize: 14,
    minTypeScale: 1.2,
    maxTypeScale: 1.25,
    positiveSteps: 5,
    negativeSteps: 2,
    relativeTo: 'viewport',
    prefix: 'decreasing-type-step'
  });
}
```

So given this, using media queries one could do something like this.

```css
/* Decreasing Type Scale */
@media screen and (max-width: 1024px) {
  /* Styles for screens up to 1024px */
  h1 {
    font-size: var(--decreasing-type-step-5);
  }
}

/* Increasing Type Scale */
@media screen and (min-width: 1025px) {
  /* Styles for screens 1025px and up */
  h1 {
    font-size: var(--type-step-5);
  }
}
```

But is that a good idea even ?
