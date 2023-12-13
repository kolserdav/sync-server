# Synchronous-Server

![License](https://img.shields.io/github/license/kolserdav/synchronous-server-node)

## Overview

The `synchronous-server` package is a Node.js module that uses Rust crates to allow the Node.js server to run synchronously. The purpose of this package is to provide a synchronously running server-side implementation of Node.js for your specific needs, such as securely modifying a single file by multiple clients.

## Requirements

To use the `synchronous-server` package, you need to ensure the following:

- Node.js is installed on your system
- Rust is installed on your system

## Installation

**Make sure to have Rust and Cargo installed on your system, as this package relies on Rust crates for its functionality.** _The fastest way to install Rust is to use Rustup https://rustup.rs/_

Install the `synchronous-server` package using npm:

```bash
npm install synchronous-server
```

## Usage

After installing the package, you can use it in your Node.js application as follows:

```javascript
const path = require("path");
const { startServer } = require("synchronous-server");

// Create an abs path to worker.js file
const workerPath = path.resolve(__dirname, "worker.js");

startServer(4001, workerPath);
```

Create file `worker.js` as follows:

```javascript
const { request, response } = require("synchronous-server");

// Wrap to async to use await
(async () => {
  // Get request
  const req = request();
  console.log(`method: ${req.method}, url: ${req.url}`);
  // An asynchronous operation will be performed synchronously
  const res = await new Promise((resolve) => {
    setTimeout(() => {
      resolve({ hello: "world", body: req.body });
    }, 0);
  });
  // Send response
  response(res);
})();
```

## API Reference

### `startServer(port: number, workerFilePath: string)`

This function starts the synchronous server on the specified port.

- `port`: The port number on which the server should listen.
- `workerFilePath`: The absolute path to the request handler file.

## License

This package is distributed under the MIT License. See the [LICENSE](LICENSE) file for more information.

## Contributions

Contributions to the `synchronous-server` package are welcome. Feel free to submit issues or pull requests on the [GitHub repository](https://github.com/kolserdav/synchronous-server-node).

## Support

For any questions or support with the `synchronous-server` package, please open an issue on the [GitHub repository](https://github.com/kolserdav/synchronous-server-node).

## Roadmap

- Support for advanced configuration options
- Performance optimization

## Versioning

This package follows the Semantic Versioning (SemVer) scheme. See the [CHANGELOG](CHANGELOG.md) for release history.
