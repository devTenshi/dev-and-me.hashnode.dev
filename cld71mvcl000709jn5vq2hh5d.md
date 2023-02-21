# Routing in NodeJS - URL module

Hello 👋

It has been a while, No blog. I started learning Node.js as a part of my *new year's resolution* to begin back-end development technology while documenting my learning in blog posts. 😉

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673966391699/86412b87-ad61-4008-82e9-9e4696243437.gif align="center")

## Contents **📜**

* Creating a basic web server 📌
    
* Routing
    
* Redirection 👀
    
* Creating a simple API
    
* Helpful Resources 👇
    

## Creating a basic web server

To build a Node.js web server, we just need the `http` module(one of the various core modules in nodeJS), which provides networking capabilities.

This server accepts and processes requests from clients who await responses as data over the Hyper Text Transfer Protocol (*HTTP* ), providing a status code and appropriate data.

The `http.createServer()` method creates an HTTP server and returns it. The function passed as the argument to `createServer()` is the callback function that will be executed each time the server receives a request. This callback function takes two arguments, `req` and `res`, which are the request and response objects, respectively.

> A callback function is a function that is passed as an argument to another function and is executed after the main function has finished its task.
> 
> The main function is responsible for triggering the callback function once it has completed its execution.

The callback function is responsible for handling the incoming request and sending a response. It will be called every time a client makes a request to the server and it's where you can handle all the logic of your server.

In this example, it's an anonymous arrow function but you can also pass a named function.

```javascript
const http = require('http');

const server = http.createServer((req, res) => {
  // Handling the request
  console.log(req.url, req.method, req.headers);
  
  // Sending a response
   res.writeHead(200, {
'Content-Type', 'text/html';
})
  res.end('<h1>Hello, World!</h1>');
});

server.listen(3000, () => {
  console.log('Server running on port 3000');
});
```

In this example, it's an anonymous arrow function. It logs the request's url, method and headers to the console and sends back a response. it sets the Content-Type to 'text/html', the status code to 200 and sends back an Html string '&lt;h1&gt;Hello, World!&lt;/h1&gt;'.

Finally, the `server.listen()` method is used to start the server and make it listen for incoming requests on port **3000.**

To reach your newly established server, enter "localhost: port" into your browser's address bar. Typically, the IP address **127.0.0.1** is used as the local host address of your device, allowing it to connect to itself.

Using the example I provided earlier, the port being used is **3000**. Therefore, in this scenario, you would enter **127.0.0.1:3000** into your browser's address bar to access the server.

With everything set up, we can save our program and execute it by running the command `node index.js` (assuming the file has been named "index.js"). The result will be visible in the terminal.

```bash
> node index.js
Server running on port 3000
Listening on http://127.0.0.1:3000
```

Let's see our response on the browser

Yay!, our server is running! 😉

## Routing

Now we created a basic web server. Did you ever wonder what would happen if we changed its URL to something else, like https://127.0.0.1:8000/products?

You would see no change in the server's behavior, it will still respond with the same message as it would with the default URL. To display different pages or perform various actions, we need to implement routing.

> Routing allows us to handle different URLs and direct them to the appropriate actions or pages.

To implement routing, we need to use a core Node.js module called the `url` module. The `url` module in Node.js can be used to parse URLs and access the different parts of the URL, such as the pathname, query string, and parameters.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1674186489192/ab8e19a2-2527-4504-a9f7-daccaf9d4b98.avif align="center")

To use this module, we need the `require` function. This function is used to import a module and make its properties and functions available for use in your code. The basic syntax for using `require` in this case of routing is:

```javascript
const url = require('url');  //require the url module
const http = require('http'); //require the http module
const server = http.createServer((req, res) => {
    console.log(req.url);    
    res.end('Hello from the server!');
});

server.listen(3000, () => {
    console.log('Listening to requests on port 3000');
});
```

When you type `console.log(req.url)` in the callback method of `http.createServer()` and then refresh the page in the browser, two lines will appear in the terminal: `/` and `/favicon.ico`

```bash
>node index.js
listening to port 3000
/
/favicon.ico
```

The first line, `/` is the URL of the current page requested by the browser from the server.

The second line, `/favicon.ico` is the URL of the browser's "favicon," which is the little symbol that appears in the browser's tab next to the page title. When the browser sends a request to the server, it also sends the favicon, which is why the terminal displays two lines.

You could use `req.url` to check the requested URL in your server and then perform different actions based on that URL. You must have seen a pattern like this in certain URLs like [https://design.com/overview?id=22&abc=3456](https://design.com/overview?id=22&abc=3456).

```javascript
const http = require('http');
const url = require('url');  //require the url module
const adrs = "https://design.com/overview?id=22&abc=3456";
let newAdrs = url.parse(adrs, true)

const server = http.createServer((req, res) => {
    console.log(req.url);
    console.log(newAdrs.search)
    console.log(newAdrs.host)
    console.log(newAdrs.pathname)
        
    res.end('Hello from the server!');
});

server.listen(3000, () => {
    console.log('Listening to requests on port 3000');
});
```

```bash
listening to requests on port 3000
/
?id=22&abc=3456
design.com
/overview
/favicon.ico
?id=22&abc=3456
design.com
/overview
```

okay; let's create a few routes.

```javascript
const server = http.createServer((req, res) => {
    const pathName = req.url;    //store the url in a variable
    if(pathName === '/' || pathName === 'overview') {
        res.end('This is the OVERVIEW!') 
    } else if(pathName === 'product') {
        res.end('This is the PRODUCT!');
    } else {
        res.end('This page cannot be found.');
    }
});
```

Sometimes when an invalid URL is requested, we can send http response status codes to the browser/client; such as 404-page not found, 401-Unauthorized, etc; using `writeHead()` . This function takes in the status code and a header( contains data about the reply we are sending back).

*You can find other http response status codes here*: [Visit](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)

```javascript
const pathName = req.url;
    if(pathName === '/' || pathName === '/overview') {
        res.end('This is the OVERVIEW!');
    } else if(pathName === '/product') {
        res.end('This is the PRODUCT!');
    } else {
        res.writeHead(404, {
            //header
            'Content-type': 'text/html',    //response will be in html format
        });
        res.end('<h1>This page cannot be found.</h1>'); //html tag as response
    }
```

> *Always restart your server and refresh the page after making changes to your code.*

## Redirection 👀

Redirection in Node.js is the process of directing a user's request to a different URL than the one they initially requested. This is done using the `http` module, which allows you to create a server and handle incoming requests.

To redirect a user to a different URL, you can use the `res.writeHead()` method on the response object, and set the `statusCode` to `302` (for a temporary redirect) or `301` (for a permanent redirect). You also need to set the `Location` header to the URL you want to redirect the user to. Here's an example:

```javascript
const http = require('http');
const server = http.createServer((req, res) => {
  res.writeHead(302, {
    'Location': 'https://www.example.com'
  });
  res.end();
});
server.listen(3000);
```

This example uses the `http.createServer()` method to create a server and listen on port 3000. When a user requests this server, the server will respond with a `302` status code and a `Location` header set to [`https://www.example.com`](https://www.example.com), which will redirect the user to that URL.

But, Keep in mind that there are several other ways to handle redirection in Node.js, such as using middleware or using a framework like `Express` which provides an easy-to-use routing mechanism and includes a `redirect()` function that can be used to perform redirects.

```javascript
const express = require('express');
const app = express();
app.get('/old-route', (req, res) => {
  res.redirect('/new-route');
});
app.listen(3000);
```

Additionally, you can also use a library like `http-proxy` to handle redirection in a more advanced way.

It's also worth noting that redirections are essential for SEO, security, and user experience. you need to make sure that you're using the appropriate status code and that you're redirecting to the correct URL, to avoid creating broken links and confusing users.

## Creating a simple API

At this moment our page is displaying Html tags, have you wondered what happens if you request some form of data from a database or external service?

This is where an API comes in 😎.

> An API, or Application Programming Interface, is a set of protocols and tools for building software and applications.

This API allows your server to communicate with an external service or database, and retrieve, update and share data. The data is usually returned in a format that is easy for humans to read and write and also easy for machines to parse and generate.

The data is provided in a `.json` file extension. A JSON(Javascript Object Notation) file is a simple text format that looks a lot like a JavaScript object.

An example of a `.json` file is:

```json
{
    "books": [
        {
            "title": "Harry Potter and the Sorcerer's Stone",
            "author": "J.K. Rowling",
            "year": 1997
        },
        {
            "title": "The Lord of the Rings",
            "author": "J.R.R. Tolkien",
            "year": 1954
        },
        {
            "title": "The Hobbit",
            "author": "J.R.R. Tolkien",
            "year": 1937
        }
    ]
}
```

To create an API, it is necessary to read the data contained within a JSON file <mark>synchronously</mark> and then parse that data into a JavaScript object using the `JSON.parse(data)` method.

Once the data has been parsed, it can then be used when implementing HTML Templating.

*I would be writing a separate article on that...*

You might be wondering, why synchronously? 😟🤔

Drumrolls 🥁🥁:

<mark>Synchronous code at the top level of our program does not block execution</mark>

Synchronous reading is a technique that allows your code to pause and wait for a file to be read before execution.

However, when a code is executed synchronously at the top level of the program, it will not prevent other code from running while it is being executed. This is used when reading a file or when waiting for a response from an external API.

In this situation, it is particularly useful when working with the callback function in the `http.createServer()` method, as it runs every time a different URL is requested, and we only want to read the file once.

This is done by storing the data in a variable.

Now let us create our basic API.

```javascript
const data = fs.readFileSync(`${__dirname}/dev-data/data.json`, 'utf-8');
const dataObj = JSON.parse(data);

const server = http.createServer((req, res) => {
    const pathName = req.url;
    if(pathName === '/' || pathName === '/overview') {
        res.end('This is the OVERVIEW!');
    } else if(pathName === '/product') {
        res.end('This is the PRODUCT!');
    } else if(pathName === '/api') {      //URL for API
        res.writeHead(200, {
       'Content-type': 'application/json'
       });   //standard header
        res.end(data);
    } else {
        res.writeHead(404, {
            'Content-type': 'text/html', //header
             });
        res.end('<h1>This page cannot be found.</h1>');
    }
});
```

The code begins by storing data from a JSON file (the name of our file in this case is `data.json`) to a variable (dataObj) while using the `JSON.parse()` , to convert the data into a JavaScript object, in this case, an array.

`__dirname` is then introduced. This variable allows the use of a file path regardless of the location of the script.

Normally, a dot in the file path represents the directory where the `node index.js` command is executed. However, when running the file from a location different from where the file is present, the variable `__dirname` can be useful and is considered best practice.

> `__dirname` tells you the absolute path of the directory containing the currently executing file.

The code also includes an additional `else-if` condition for the API route. This is where the data from the JSON file is sent to the server using the `res.end()` method, which takes a string as a parameter. The browser is also informed about the type of data being sent, with the use of a header.

With these few steps, you should be able to create your web server, route through the server, create a simple API and read the data from the API.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1674310683061/5260aa58-def3-4475-b749-4c3f5b139c7c.gif align="center")

## Helpful Resources 👇

* [Understanding \_\_dirname and \_\_filename](https://remarkablemark.org/blog/2017/04/12/nodejs-module-dirname-filename/)
    
* Read [Documentation on NodeJS](https://nodejs.org/dist/latest-v14.x/docs/api/)
    
* [HTTP headers, methods and status codes](https://www.youtube.com/watch?v=iYM2zFP3Zn0)
    
* [Understanding file system paths](https://www.youtube.com/watch?v=7UIXzCEqgas&ab_channel=MicrosoftDeveloper)
    
* [Master NodeJS, Express and MongoDB - Udemy Course](https://www.udemy.com/course/nodejs-express-mongodb-bootcamp/)
    

You've reached the end of the article! 🎉  
Please leave feedback in the comment section and stay tuned for the next post! 🚀  
Happy Learning💡