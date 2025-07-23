# no-browser

A utility package that prevents modules from being imported in browser/client environments using Node.js conditional exports.

## Installation

```bash
npm install no-browser
```

## Usage

Import this package at the top of any module that should only run in server-side or Node.js environments:

```javascript
import 'no-browser';

// Your server-only code here
import fs from 'fs';
import path from 'path';

export function readServerConfig() {
  return fs.readFileSync(path.join(process.cwd(), 'config.json'), 'utf8');
}
```

When bundlers or build tools process this code for browser environments, they will encounter an error preventing the module from being included in client-side bundles.

## How it works

The package leverages Node.js conditional exports to serve different files based on the environment:

- **Browser environments**: Serves `index.js` which throws an error with a descriptive message
- **Node.js/server environments**: Serves `empty.js` which is a no-op module

The conditional export configuration in `package.json`:

```json
{
  "exports": {
    ".": {
      "browser": "./index.js",
      "default": "./empty.js"
    }
  }
}
```

## Why use this?

This package is inspired by similar patterns used by frameworks like Next.js with their `server-only` package. It's useful for:

- Preventing accidental inclusion of server-side code in client bundles
- Catching build-time errors before deployment
- Ensuring sensitive server operations don't leak to the client
- Making explicit the server-only nature of modules

## Similar packages

- [`server-only`](https://www.npmjs.com/package/server-only) - React Server Components specific version
- Manual conditional exports in your own packages
- Build tool configurations to exclude server modules

## Error message

When imported in a browser environment, you'll see:

```
Error: This module cannot be imported from a browser/client environment. It should only be used in server-side or Node.js environments.
```

## License

MIT
