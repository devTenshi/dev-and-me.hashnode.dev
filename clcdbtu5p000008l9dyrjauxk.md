# Beginner: Use of basic console module in NodeJS

Hello learners and welcome to my first blog of the year. In this blog, we are going to learn how to use the most common console module to display output on the command line in NodeJs.

NodeJs is an open-source runtime environment for Javascript. Node makes it possible for developers to use Javascript for both server-side and mobile applications.

For this tutorial, you would need the following:

* A code editor (I would be using vscode)
    
* Node installed (currently using v19.3.0)
    
    [Install node](https://kinsta.com/blog/how-to-install-node-js/)
    

### The Command line

A command line or preferably a command-line interface (CLI) is a text-based editing environment, used to run programs, interact, and perform operations on the computer.

This environment is used to execute and test Javascript codes

To run a NodeJS code on the command line, simply type the `node` command (this only runs if you have nodeJs installed) and the name of the file you wish to execute.

For example; if the name of your file is `script.js,` you can call it by typing

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672569664412/fd396b63-d911-4c87-98eb-5a5be15e9f22.png align="left")

### The console

To interact with the command line, Node provides a core module known as the console module. This console is similar to the console provided by the web browser.

syntax:  
`console.log(" ")`

The `console` module has a lot of [methods](https://nodejs.org/api/console.html) but the most used method is `console.log()`.

This method is used to print whatever message is passed into it, on the console.

`console.log()` can take in multiple parameters that can be an object, array or any message and NodeJS will print them all.

***When passing an argument in a function:***

![output when passing a function](https://cdn.hashnode.com/res/hashnode/image/upload/v1672571478604/6b3a9a36-1349-49f6-8c28-a1cae941525e.png align="center")

***When passing multiple variables:***

![output when passing multiple variables](https://cdn.hashnode.com/res/hashnode/image/upload/v1672571596107/43b38e93-5f8a-4ff3-9d65-4941103fd403.png align="center")

***when passing an array of strings:***

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672573615359/0f2b9269-d1b6-402a-b0af-eba24c8a1bf8.png align="center")

## **Conclusion**

In conclusion, we learned the basic use of a command line in NodeJS and how to run a file in its environment.

Additionally, we also talked about the console module and using the`.log()` method to output data on the command line in NodeJS.

If this is helpful, leave a like 👍 and drop a comment 😎

### **References**

* [Output to the command line using nodeJS](https://nodejs.dev/en/learn/output-to-the-command-line-using-nodejs/)
    
* [Steps to installing NodeJS](https://kinsta.com/blog/how-to-install-node-js/)