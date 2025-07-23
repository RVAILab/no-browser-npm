# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a utility npm package called "no-browser" that serves as a marker to prevent modules from being imported in browser/client environments. It's designed to be imported by server-only packages to ensure they throw an error when accidentally bundled for the browser.

## Architecture

The package uses Node.js conditional exports to serve different files based on the environment:

- **index.js**: Contains an error that throws when imported in browser environments
- **empty.js**: An empty file (no-op) that loads in Node.js/server environments
- **package.json exports**: Uses the "browser" condition to serve index.js in browsers and empty.js by default

The core mechanism is in package.json:
```json
"exports": {
  ".": {
    "browser": "./index.js",
    "default": "./empty.js"
  }
}
```

## Development Commands

This is a simple utility package with no build process, test suite, or complex tooling. The package consists of static files that are published directly.

- **Publishing**: Standard `npm publish` (no pre-build steps required)
- **Testing**: Manual testing would involve importing the package in different environments

## File Structure

- `index.js`: Error-throwing module for browser environments
- `empty.js`: Empty module for server environments  
- `package.json`: Main configuration with conditional exports
- `README.md`: User documentation explaining usage