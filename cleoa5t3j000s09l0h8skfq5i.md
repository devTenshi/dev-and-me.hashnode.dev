# HTML Templating in NodeJs

HTML templating is a technique that allows us to create a base HTML structure and use placeholders to dynamically generate content based on data retrieved from our JSON file.

Let's consider a hypothetical instance where our website consists of numerous product cards, each containing specific product details that are retrieved from the JSON file.

Now, if we were to add or remove any products from our JSON file, how would we update the corresponding cards on the front-end dynamically?

Considering our content-based data is stored in a JSON file, we can proceed with creating reusable templates from our existing HTML code.

### Step 1: Building the templates

As a developer, you're probably familiar with the concept of serving dynamic web content. One way to achieve this is by using templates.

We would create two HTML templates, one for the product overview page and one for the individual product cards.

The first template `template-card.html` is used as a blueprint for the individual product cards, and the second `template-overview.html` is used as a blueprint for the overview page. These templates contain placeholders that will be replaced with actual content when the page is requested by a user.

Ensure that your placeholder does not contain any symbols that are part of the HTML code. A commonly used syntax for placeholders is `{%PLACEHOLDER_NAME%}`.

Here is `template-card.html` our first template used as a blueprint to create as many cards as needed dynamically.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677480282284/5544facd-9889-4816-b7d8-149f2ebcbf4c.png align="center")

Remember to have your constructed templates stored in a different folder, like this:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677479315451/3598815b-4b47-4ba6-a814-6090b2c9009f.png align="center")

As this card will serve as a template, the information contained within it should be replaced with placeholders as well. Once the placeholders have been added, the card will resemble the following:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677479898580/cfd017f8-2404-44d6-a7a2-1290d72807d9.png align="center")

> The anchor tag contains an `href` link that includes a placeholder for an ID. This indicates that each card or product in our JSON file has a distinct ID. These IDs are unique and will be utilized in identifying each product during routing.

Also, when we need to style elements based on their category, CSS classes and IDs can be substituted with placeholders as is done in the image examples. This approach can prove especially useful in such cases.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677480896175/7fc81e25-0202-4103-8ca2-95af6ef63bb8.png align="center")

In this example, we have substituted our template card with a placeholder. It's important to keep in mind that we will generate multiple cards dynamically using this single template card.

**Note** This is our second template card, `template-overview.html`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677484998640/fb89a8ca-369e-4acb-b6a5-e92ef1654d1c.gif align="center")

### Step 2: Filling the templates

Here comes the fun part, filling our templates by replacing our placeholders with actual content.

When a user requests a URL, the code reads the relevant template file (either `template-overview.html` or `template-card.html`) synchronously, fills it dynamically with content from a JSON file, and sends back the relevant content as a response to the user.

This is achieved through the use of the `replaceTemplate` function, which replaces the placeholders in the template with actual content.

```javascript
// SECOND STEP:
const replaceTemplate = (temp, product) => {
    let output = temp.replace(/{%PRODUCTNAME%}/g, product.productName);
    output = output.replace(/{%IMAGE%}/g, product.image);
    output = output.replace(/{%PRICE%}/g, product.price);
    output = output.replace(/{%ID%}/g, product.id); 
     // /g is a regex global flag
    return output;
}

// FIRST STEP:
const tempOverview = fs.readFileSync(`${__dirname}/templates/template-overview.html`, 'utf-8');
const tempCard = fs.readFileSync(`${__dirname}/templates/template-card.html`, 'utf-8');
const data = fs.readFileSync(`${__dirname}/dev-data/data.json`, 'utf-8');
const dataObj = JSON.parse(data);

// THIRD STEP:
const server = http.createServer((req, res) => {
    const pathName = req.url;

    //FOURTH STEP:
    //Here is the Overview
    if(pathName === '/' || pathName === '/overview') {
        res.writeHead(200, {'Content-type': 'text/html'});
        const cardsHtml = dataObj.map(el => replaceTemplate(tempCard, el)).join('');
        const output = tempOverview.replace('{%PRODUCT_CARDS%', cardsHtml);

        res.end(output);

        //API
    } else if(pathName === '/api') {
        res.writeHead(200, {'Content-type': 'application/json'});
        res.end(data);
    // Not Found
    } else {
        res.writeHead(404, {
            'Content-type': 'text/html', //standard header
            'my-header': 'hello-world'
        });
        res.end('<h1>This page cannot be found.</h1>');
    }
});

server.listen(8000, '127.0.0.1', () => {
    console.log('Listening to requests on port 8000');
});
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677484813018/297e96e0-583a-4348-8241-19f8f88e4aec.gif align="center")

Don't worry, we will take a closer look at the big block of code up there and figure out what it does in simpler terms.

* First, read the two HTML template files and the product data that is stored in a JSON file
    
* Second, define a function that replaces placeholders in the templates with product-specific data. Here, our function is named `replaceTemplate`
    
* Third, listen to incoming HTTP requests and check the `pathname` of the request URL
    
* Fourth, If the `pathname` is `/` or `/overview`, generate HTML code for each product card by replacing placeholders in the `tempCard` template using the `replaceTemplate` function and the product data from the JSON file.  
    The resulting HTML for each card is then concatenated to create the `cardsHtml` string. The `tempOverview` template is then modified to include the `cardsHtml` string and the resulting HTML code is sent back as the response
    
* Also, if the `pathname` is `/api` it sends back the product data in JSON format as the response
    
* Finally, if the `pathname` is anything else, sends back a 404 error message
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677486090088/81f9cb8e-4510-4342-a79a-e555a6cb8f7e.gif align="center")

Wow, that code did look like a lot, but if we look closely and take it one step at a time, it's not that complicated. All it's doing is replacing some special words with real information and sending it back to the website so people can see it!

## Benefits of HTML templating

HTML templating offers several benefits that make it a popular choice among web developers:

1. By utilizing HTML templating, we separate content from the presentation allowing developers to generate reusable templates that can handle varying amounts of data from multiple sources, and maintain multiple copies of similar code.
    
2. HTML templates provide a standard structure for presenting data, improving user experience and easy navigation on the site.
    
3. The flexibility of templating makes it easier to modify the underlying data. This saves time and effort, as developers don't need to change the HTML code manually.
    
4. Since HTML templates are reusable, they are easier to maintain and update. Changes to the underlying data can be made without modifying the template code, which reduces the likelihood of errors.
    
5. HTML templating can handle large amounts of data without compromising performance. This makes it an ideal choice for websites with a significant amount of dynamic content.
    

In summary, HTML templating is an efficient, consistent, flexible, and scalable technique that simplifies the development and maintenance of dynamic web content. By separating content from presentation, HTML templating enables developers to create reusable templates that can handle varying amounts of data, without having to hard-code the content into each page.

## Bonus Section:

There are several other templating engines available in Node.js, such as EJS, Pug (formerly known as Jade), Handlebars, and Mustache, among others. To use a templating engine in Node.js, you'll need to install it via npm and then require it in your code. These engines provide a way to generate HTML by inserting data into placeholders within the template.

You've reached the end of the article! 🎉 Hope you enjoyed this post and learned something new 💡.  
Here is a gift for you **🎁,** Thanks for sticking around.

## **Resources for You 🎁**

* [**Understanding JSON**](https://www.youtube.com/watch?v=iiADhChRriM&ab_channel=WebDevSimplified)
    
* [**More about filesystem paths**](https://www.youtube.com/watch?v=7UIXzCEqgas&ab_channel=MicrosoftDeveloper)
    
* [**HTTP Headers**](https://www.youtube.com/watch?v=iYM2zFP3Zn0&ab_channel=TraversyMedia)
    
* [**JavaScript String replace() Method**](https://www.w3schools.com/jsref/jsref_replace.asp)
    
* [**JavaScript Array join() Method**](https://www.w3schools.com/jsref/jsref_join.asp)
    
* [**JavaScript Array map() Method**](https://www.w3schools.com/jsref/jsref_map.asp)
    
* [**Placeholders in JavaScript**](https://mightytechno.com/replace-placeholders-in-javascript/)
    
* [RegEx in JS](https://www.w3schools.com/jsref/jsref_obj_regexp.asp)
    
* [**JavaScript Array Methods**](https://www.w3schools.com/jsref/jsref_obj_array.asp)