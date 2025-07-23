# no-browser

A marker package to prevent modules from being imported in browser/client environments.

## Usage

Import this package at the top of any module that should only run in server-side or Node.js environments:

```javascript
import 'no-browser';

// Your server-only code here
```

When bundlers or build tools detect the browser condition, they will throw an error preventing the module from being included in client-side bundles.

## How it works

The package uses conditional exports to serve different files based on the environment:
- In browser environments: throws an error
- In Node.js/server environments: loads an empty module (no-op)

## License

MIT# no-browser-npm
