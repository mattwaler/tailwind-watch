# Tailwind Watch

A dead-simple package to intelligently watch your project for Tailwind-specific files and rebuild when they change.

Keep Tailwind separate from your bundling process, if you're even still doing that kind of thing.

## Why might you use this?

- Tired of configuring Tailwind and PostCSS through bundlers like Webpack and Rollup
- You've evolved past bundlers to Skypack but still want to use Tailwind
- Want control over all PostCSS and Tailwind configuration via configuration files in project root
- Want intelligent watching and building, depending on `.env` variables and `process.env.NODE_ENV`

## Installation & Usage

First, install the package:
```
npm i -D @mattwaler/tailwind-watch
```

If you don't already, make sure you've at least got PostCSS and Tailwind installed:
```
npm i -D postcss postcss-cli tailwindcss
```

Then, add input and output values to your `.env` file, or create it if it does not already exist, like so:

```dotenv
TAILWIND_IN=src/input.css
TAILWIND_OUT=dist/output.css
```

Finally, add the proper commands to your `package.json` scripts. This works best by tying your existing commands together with something like `npm-run-all`. Here's an example of how you might tie this package together with Eleventy:

```json
{
  "scripts": {
    "build": "NODE_ENV=production npm-run-all build:*",
    "build:eleventy": "eleventy",
    "build:tailwind": "tailwind-watch",
    "dev": "npm-run-all dev:*",
    "dev:eleventy": "eleventy --serve --quiet",
    "dev:tailwind": "tailwind-watch"
  }
}
```

This package will do one of two things, depending on the value of `process.env.NODE_ENV`:

1. If the value is `production`, it will ***ONLY*** build the output file.
2. If the value is anything else, it will build the output file ***AND*** start the watcher.

Happy Tailwinding!