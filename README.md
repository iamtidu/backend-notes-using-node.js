# 1. Introduction to Node.js

## What is `Node.js`?

Node.js is an open-source, cross-platform JavaScript runtime environment that allows developers to execute JavaScript code on the server side. It uses the V8 JavaScript engine (the same one used by Google Chrome) to execute code and includes a library of various JavaScript modules to help simplify the development of web applications and other types of software.

## Installation and Setup
To install Node.js, follow these steps:
1.	Download Node.js:
- Go to the official [Node.js](https://nodejs.org/en) website.
- Download the latest LTS (Long Term Support) version for your operating system.

2.	Install Node.js:
-	Run the installer and follow the setup wizard.
-	After installation, verify it by opening a terminal (Command Prompt, PowerShell, or terminal on Mac/Linux) and typing:
`node -v`
`npm -v`
- you should see the version numbers of Node.js and npm (Node Package Manager), indicating a successful installation.
### Understanding Node.js Architecture and Event-Driven Programming
Node.js is designed to be event-driven and non-blocking, which makes it ideal for building scalable and high-performance applications.
- Single-Threaded Event Loop: Node.js operates on a single-threaded event loop architecture, meaning it uses a single thread to handle all incoming requests. The event loop allows Node.js to perform non-blocking I/O operations, handling multiple operations concurrently.
- Event-Driven: Node.js uses an event-driven architecture, where events are emitted and handled by callback functions. This approach allows the server to remain responsive and handle high concurrency.

## 2. Basic Concepts

### Node.js REPL (Read-Eval-Print Loop)
The Node.js REPL is an interactive shell that allows you to execute JavaScript code and see the results immediately. It's useful for experimenting and debugging code snippets.

To start the REPL, open your terminal and type:

 `node`

You can now type JavaScript code and see the output:
``` javascript
const message = "Hello, Node.js!";
console.log(message);
Hello, Node.js!
```


### Global Objects and Core Modules
Node.js provides several global objects and built-in modules that you can use without requiring them explicitly.
#### Global Objects:
- __dirname: The directory name of the current module.
- __filename: The file name of the current module.
- module: The current module.
- exports: The object that's exposed as a module.
 
 Example:
``` javascript
console.log(__dirname);
console.log(__filename);
console.log(module);
```
#### Core Modules:
- fs: File system module.
- http: HTTP module.
- path: Path module.
 Example:

``` javascript
const fs = require('fs');
const path = require('path');
const filePath = path.join(__dirname, 'example.txt');
fs.writeFileSync(filePath, 'Hello, world!');
```

### Creating Your First Node.js Application
Let's create a simple Node.js application that prints "Hello, World!" to the console.
1.	Create a new directory for your project and navigate into it:
```javascript
mkdir my-node-app
cd my-node-app
```
2.	Create a new file named app.js and open it in your favorite text editor. Add the following code:
```javascript
console.log('Hello, World!');
```
3.	Save the file and run it using Node.js:
```javascript
node app.js
```

> You should see the output:
> Hello, World!


### Working with the console and process Objects
- **Console Object:** The console object provides methods for writing to the standard output and standard error streams.
```javascript	
console.log('This is a log message.');
console.error('This is an error message.');
console.warn('This is a warning message.');
```
- **process Object:** The process object provides information and control over the current Node.js process. It can be used to handle command-line arguments, environment variables, and more.
```javascript
console.log('Current directory:', process.cwd());
console.log('Node.js version:', process.version);
console.log('Environment variables:', process.env);

example:
// Handling command-line arguments
process.argv.forEach((val, index) => {
 	 console.log(`${index}: ${val}`);
});

// Exiting the process
process.exit(0);
```
## 3. Modules and Packages
### Understanding Modules in Node.js
In Node.js, a module is a reusable piece of code encapsulated in a file. Each module in Node.js has its own context, so it cannot interfere with other modules. This helps to maintain a clean namespace and promotes modular code.

Modules can be of three types:
1.	***Built-in modules:*** These are provided by Node.js out of the box (e.g., fs, http, path).
2.	***Third-party modules:*** These are created by the community and can be installed using npm.
3.	***Custom modules:*** These are created by the developer.

#### Built-in Modules
Node.js comes with a set of built-in modules that provide a wide range of functionality.
1.	**File System (fs) Module:** The fs module allows you to interact with the file system in a way modeled on standard POSIX functions.
```javascript
//Example: Reading a file asynchronously.
const fs = require('fs');

fs.readFile('example.txt', 'utf8', (err, data) => {
  if (err) {
    console.error(err);
    return;
  }
  console.log(data);
});
```
2.	**HTTP Module:** The http module allows you to create an HTTP server and handle HTTP requests and responses.
```javascript
//Example: Creating a simple HTTP server.
 
const http = require('http');
const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello, World!\n');
});

server.listen(3000, '127.0.0.1', () => {
  console.log('Server running at http://127.0.0.1:3000/');
});
```
3.	**Path Module:** The path module provides utilities for working with file and directory paths.

```javascript
//Example: Working with paths.
 
const path = require('path');
const filePath = path.join(__dirname, 'example.txt');
console.log(filePath);
console.log(path.basename(filePath));
console.log(path.extname(filePath));
```
### Creating Custom Modules
You can create your own modules to encapsulate and reuse code. A module is typically a JavaScript file that exports one or more objects, functions, or variables.
Example: Creating and using a custom module.
1.	**Creating a custom module:** Create a file named math.js with the following code:
```javascript
// math.js
function add(a, b) {
  return a + b;
}
function subtract(a, b) {
  return a - b;
}

module.exports = {
  add,
  subtract
};

```
2.	 **Using the custom module:** Create another file named app.js and use the math module:
```javascript
// app.js
const math = require('./math');
console.log('2 + 3 =', math.add(2, 3));
console.log('5 - 2 =', math.subtract(5, 2));
```
### Using npm (Node Package Manager)

npm is the default package manager for Node.js. It allows you to install and manage third-party libraries (packages) and your own packages.

1.	**Initializing a Project:** To start using npm in your project, you need to create a package.json file. This file holds metadata about your project and lists its dependencies.

`npm init`

Follow the prompts to create the package.json file.

2.	**Installing Packages:** You can install packages using the npm install command. By default, npm installs packages locally (in a node_modules directory within your project).
> Example: Installing the express package.

`npm install express`

This command adds express to your node_modules directory and updates package.json to include express as a dependency.

3.	**Using Installed Packages:** Once installed, you can use the package in your project by requiring it.

```javascript
//Example: Using express to create a simple web server.
 
const express = require('express');
const app = express();

app.get('/', (req, res) => {
  res.send('Hello, World!');
});

app.listen(3000, () => {
  console.log('Server is running on http://localhost:3000');
});
```
### Managing Packages:

**Updating Packages:** You can update packages to their latest versions.

`npm update`

**Uninstalling Packages:** You can remove packages from your project.

`npm uninstall express`

**Global Packages:** You can install packages globally to use them across multiple projects.

`npm install -g nodemon`

**Development Dependencies:** Some packages are only needed during development. You can install these as development dependencies.

`npm install --save-dev jest`

By understanding modules and packages, you can effectively manage and utilize the vast ecosystem of libraries available in the Node.js community, making your development process more efficient and modular.

## File System

The fs (File System) module in Node.js is a core module that provides an API for interacting with the file system. It includes methods for reading, writing, appending, renaming, deleting files, and working with directories. Here’s a detailed explanation of its various functionalities with examples:
##### Importing the fs Module
To use the fs module, you need to import it first:
```javascript
const fs = require('fs');
```
### Reading Files

#### Asynchronous Reading
 The asynchronous fs.readFile method reads the contents of a file without blocking the event loop. It takes a callback function that is called when the file has been read.

 ```javascript
const fs = require('fs');

fs.readFile('example.txt', 'utf8', (err, data) => {
  if (err) {
    console.error('Error reading file:', err);
    return;
  }
  console.log('File content:', data);
});	
```
#### Synchronous Reading
 The synchronous fs.readFileSync method reads the contents of a file and blocks the event loop until the file is read completely.

```javascript
const fs = require('fs');

try {
  const data = fs.readFileSync('example.txt', 'utf8');
  console.log('File content:', data);
} catch (err) {
  console.error('Error reading file:', err);
}
```
### Writing Files

#### Asynchronous Writing
 The asynchronous fs.writeFile method writes data to a file without blocking the event loop. It takes a callback function that is called when the file has been written.
```javascript
const fs = require('fs');

const data = 'Hello, Node.js!';
fs.writeFile('example.txt', data, (err) => {
  if (err) {
    console.error('Error writing file:', err);
    return;
  }
  console.log('File has been written');
});
```

#### Synchronous Writing
 The synchronous fs.writeFileSync method writes data to a file and blocks the event loop until the file is written completely.
```javascript
const fs = require('fs');

const data = 'Hello, Node.js!';
try {
  fs.writeFileSync('example.txt', data);
  console.log('File has been written');
} catch (err) {
  console.error('Error writing file:', err);
}
```

### Appending to Files
#### Asynchronous Appending
 The asynchronous fs.appendFile method appends data to a file without blocking the event loop.

```javascript
const fs = require('fs');

const data = '\nAppending some text!';
fs.appendFile('example.txt', data, (err) => {
  if (err) {
    console.error('Error appending to file:', err);
    return;
  }
  console.log('Data has been appended');
});
```


#### Synchronous Appending
 The synchronous fs.appendFileSync method appends data to a file and blocks the event loop until the data is appended completely.
```javascript
const fs = require('fs');

const data = '\nAppending some text!';
try {
  fs.appendFileSync('example.txt', data);
  console.log('Data has been appended');
} catch (err) {
  console.error('Error appending to file:', err);
}
```

### Deleting Files

#### Asynchronous Deletion
The asynchronous fs.unlink method deletes a file without blocking the event loop.
```javascript 
const fs = require('fs');

fs.unlink('example.txt', (err) => {
  if (err) {
    console.error('Error deleting file:', err);
    return;
  }
  console.log('File has been deleted');
});
```

#### Synchronous Deletion
The synchronous fs.unlinkSync method deletes a file and blocks the event loop until the file is deleted completely.
```javascript
const fs = require('fs');

try {
  fs.unlinkSync('example.txt');
  console.log('File has been deleted');
} catch (err) {
  console.error('Error deleting file:', err);
}
```

### Working with Directories

#### Creating Directories

**Asynchronous Creation:**
```javascript
const fs = require('fs');

fs.mkdir('newDir', { recursive: true }, (err) => {
  if (err) {
    console.error('Error creating directory:', err);
    return;
  }
  console.log('Directory created');
});
```

**Synchronous Creation:**
```javascript
const fs = require('fs');

try {
  fs.mkdirSync('newDir', { recursive: true });
  console.log('Directory created');
} catch (err) {
  console.error('Error creating directory:', err);
}
```
#### Reading Directories
**Asynchronous Reading:**
```javascript
const fs = require('fs');

fs.readdir('.', (err, files) => {
  if (err) {
    console.error('Error reading directory:', err);
    return;
  }
  console.log('Directory contents:', files);
});
```
**Synchronous Reading:**

```javascript
const fs = require('fs');

try {
  const files = fs.readdirSync('.');
  console.log('Directory contents:', files);
} catch (err) {
  console.error('Error reading directory:', err);
}
```
#### Removing Directories
**Asynchronous Removal:**

```javascript
const fs = require('fs');

fs.rmdir('newDir', { recursive: true }, (err) => {
  if (err) {
    console.error('Error removing directory:', err);
    return;
  }
  console.log('Directory removed');
});
```

**Synchronous Removal:**

```javascript
const fs = require('fs');

try {
  fs.rmdirSync('newDir', { recursive: true });
  console.log('Directory removed');
} catch (err) {
  console.error('Error removing directory:', err);
}
```

#### Renaming Files
**Asynchronous Renaming**
The asynchronous fs.rename method renames a file or directory without blocking the event loop.

```javascript
const fs = require('fs');

fs.rename('example.txt', 'newExample.txt', (err) => {
  if (err) {
    console.error('Error renaming file:', err);
    return;
  }
  console.log('File renamed');
});
```
**Synchronous Renaming**
The synchronous fs.renameSync method renames a file or directory and blocks the event loop until the renaming is complete.

```javascript
const fs = require('fs');
try {
  fs.renameSync('example.txt', 'newExample.txt');
  console.log('File renamed');
} catch (err) {
  console.error('Error renaming file:', err);
}
```
#### Copying Files
**Asynchronous Copying**
The asynchronous fs.copyFile method copies a file without blocking the event loop.

```javascript
const fs = require('fs');

fs.copyFile('source.txt', 'destination.txt', (err) => {
  if (err) {
    console.error('Error copying file:', err);
    return;
  }
  console.log('File copied');
});
```
**Synchronous Copying**
 The synchronous fs.copyFileSync method copies a file and blocks the event loop until the copying is complete.

```javascript
const fs = require('fs');

try {
  fs.copyFileSync('source.txt', 'destination.txt');
  console.log('File copied');
} catch (err) {
  console.error('Error copying file:', err);
}
```
#### Checking File/Directory Existence
**Asynchronous Checking**
 The asynchronous fs.access method checks the accessibility of a file or directory without blocking the event loop.
```javascript
const fs = require('fs');

fs.access('example.txt', fs.constants.F_OK, (err) => {
  console.log(`${err ? 'File does not exist' : 'File exists'}`);
});
```
**Synchronous Checking**
 The synchronous fs.accessSync method checks the accessibility of a file or directory and blocks the event loop until the check is complete.
```javascript
const fs = require('fs');
try {
  fs.accessSync('example.txt', fs.constants.F_OK);
  console.log('File exists');
} catch (err) {
  console.error('File does not exist');
}
```
#### Getting File/Directory Stats
**Asynchronous Stats**
The asynchronous fs.stat method retrieves the stats of a file or directory without blocking the event loop.

```javascript
const fs = require('fs');

fs.stat('example.txt', (err, stats) => {
  if (err) {
    console.error('Error getting stats:', err);
    return;
  }
  console.log('File stats:', stats);
});
```
**Synchronous Stats**
The synchronous fs.statSync method retrieves the stats of a file or directory and blocks the event loop until the retrieval is complete.

```javascript
const fs = require('fs');

try {
  const stats = fs.statSync('example.txt');
  console.log('File stats:', stats);
} catch (err) {
  console.error('Error getting stats:', err);
}
```
### Asynchronous vs Synchronous File Operations
#### Asynchronous Operations:
- Non-blocking and do not wait for the operation to complete.
- Use callbacks or promises to handle the result of the operation.
- Preferred for I/O-bound tasks to keep the application responsive.
```javascript
//Example:
const fs = require('fs');

fs.readFile('example.txt', 'utf8', (err, data) => {
  if (err) {
    console.error('Error reading file:', err);
    return;
  }
  console.log('File content:', data);
});

console.log('This will print before the file content');
```
#### Synchronous Operations:
- Blocking and wait for the operation to complete before moving to the next line of code.
- Simplify code structure since they do not require callbacks or promises.
- Not recommended for I/O-bound tasks in a production environment due to potential performance issues.

```javascript
//Example:
const fs = require('fs');

try {
  const data = fs.readFileSync('example.txt', 'utf8');
  console.log('File content:', data);
} catch (err) {
  console.error('Error reading file:', err);
}

console.log('This will print after the file content');
```
Understanding the differences between asynchronous and synchronous file operations helps you choose the right approach based on your application's needs. Asynchronous operations are generally preferred for I/O-bound tasks to maintain the application's responsiveness, while synchronous operations can be useful for simple scripts or when the blocking behavior is desired.

> Note read file using http:

```javascript 
const http = require('http');
const fs = require('fs');

http.createServer((req,res)=>{
  fs.readFile('./index.html',(err,data)=>{
      res.end(data);
  })
}).listen(3000)
```

## HTTP Module
The http module in Node.js allows you to create a web server that can handle HTTP requests and responses. This is essential for building web applications and services. Below, we will cover the key concepts related to creating a basic HTTP server, handling requests and responses, routing and serving static files, and performing CRUD (Create, Read, Update, Delete) operations.
#### Creating a Basic HTTP Server
To create a basic HTTP server, you need to use the http module. Here’s a simple example:

```javascript
const http = require('http');

const server = http.createServer((req, res) => {
  res.writeHead(200, { 'Content-Type': 'text/plain' });
  res.end('Hello, World!\n');
});

const port = 3000;

server.listen(port, () => {
  console.log(`Server running at http://localhost:${port}/`);
});
```

### Handling Requests and Responses
When handling requests and responses, you can access various properties and methods of the req (request) and res (response) objects.
**Accessing Request Data**
- ***URL:*** `req.url`
- ***HTTP Method:*** `req.method`
- ***Headers:*** `req.headers`
  
**Sending Response Data**

- ***Set Status Code:*** `res.statusCode`
- ***Set Headers:*** `res.setHeader`
- ***Send Response Body:*** `res.write and res.end`

```javascript
//Example:
const http = require('http');

const server = http.createServer((req, res) => {
  const url = req.url;
  const method = req.method;

  if (url === '/') {
    res.writeHead(200, { 'Content-Type': 'text/html' });
    res.write('<html><body><h1>Home Page</h1></body></html>');
    return res.end();
  }

   if (url === '/about') {
    res.writeHead(200, { 'Content-Type': 'text/html' });
    res.write('<html><body><h1>About Page</h1></body></html>');
    return res.end();
  }

  res.writeHead(404, { 'Content-Type': 'text/html' });
  res.write('<html><body><h1>404 Not Found</h1></body></html>');
  res.end();
});

const port = 3000;
server.listen(port, () => {
  console.log(`Server running at http://localhost:${port}/`);
});
```

### Routing and Serving Static Files
To handle routing more efficiently and serve static files, you can use additional modules like fs for file system operations.

**Simple Routing Example**

```javascript
const http = require('http');
const fs = require('fs');
const path = require('path');

const server = http.createServer((req, res) => {
  const url = req.url;
  const method = req.method;

  if (url === '/') {
    fs.readFile(path.join(__dirname, 'public', 'index.html'), (err, content) => {
      if (err) {
        res.writeHead(500);
        res.end('Error loading file');
      } else {
        res.writeHead(200, { 'Content-Type': 'text/html' });
        res.end(content);
      }
    });
  } else if (url === '/about') {
    fs.readFile(path.join(__dirname, 'public', 'about.html'), (err, content) => {
      if (err) {
        res.writeHead(500);
         res.end('Error loading file');
      } else {
        res.writeHead(200, { 'Content-Type': 'text/html' });
        res.end(content);
      }
    });
  } else {
    res.writeHead(404, { 'Content-Type': 'text/html' });
    res.end('<h1>404 Not Found</h1>');
  }
});

const port = 3000;
server.listen(port, () => {
  console.log(`Server running at http://localhost:${port}/`);
});
```
### CRUD Operations in fs
For CRUD operations, you typically work with data, often stored in a database or in-memory. Below is a simple example using an in-memory data structure to perform CRUD operations.
#### In-Memory Data Store Example

```javascript
const http = require('http');

let items = [];

const server = http.createServer((req, res) => {
  const url = req.url;
  const method = req.method;

  if (url === '/items' && method === 'GET') {
    res.writeHead(200, { 'Content-Type': 'application/json' });
    res.end(JSON.stringify(items));
  } else if (url === '/items' && method === 'POST') {
    let body = '';
    req.on('data', chunk => {
      body += chunk.toString();
    });
    req.on('end', () => {
      const newItem = JSON.parse(body);
      items.push(newItem);
      res.writeHead(201, { 'Content-Type': 'application/json' });
      res.end(JSON.stringify(newItem));
     });
  } else if (url.startsWith('/items/') && method === 'PUT') {
    const id = url.split('/')[2];
    let body = '';
    req.on('data', chunk => {
      body += chunk.toString();
    });
    req.on('end', () => {
      const updatedItem = JSON.parse(body);
      items = items.map(item => (item.id === id ? updatedItem : item));
      res.writeHead(200, { 'Content-Type': 'application/json' });
      res.end(JSON.stringify(updatedItem));
    });
  } else if (url.startsWith('/items/') && method === 'DELETE') {
    const id = url.split('/')[2];
    items = items.filter(item => item.id !== id);
    res.writeHead(204, { 'Content-Type': 'application/json' });
    res.end();
  } else {
    res.writeHead(404, { 'Content-Type': 'application/json' });
    res.end(JSON.stringify({ message: 'Not Found' }));
  }
});

const port = 3000;
server.listen(port, () => {
  console.log(`Server running at http://localhost:${port}/`);
});
```
- **Creating a Basic HTTP Server:** Use the http.createServer method to create a server and listen on a specific port.
- **Handling Requests and Responses:** Access request data and send responses using req and res objects.
- **Routing and Serving Static Files:** Handle different routes and serve static files using the fs module.
- **CRUD Operations:** Perform `Create`, `Read`, `Update`, and `Delete` operations on data using ***HTTP methods*** like `GET`, `POST`, `PUT`, and `DELETE`.
  
!Bingo !
