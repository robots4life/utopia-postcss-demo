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
