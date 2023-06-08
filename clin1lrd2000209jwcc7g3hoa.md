---
title: "REST APIs."
seoTitle: "Rest APIs"
seoDescription: "All about rest api principles, restful apis and authentication methods"
datePublished: Thu Jun 08 2023 11:15:44 GMT+0000 (Coordinated Universal Time)
cuid: clin1lrd2000209jwcc7g3hoa
slug: all-about-rest-principles-restful-apis-authentication-methods
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1684765886063/5d7442f1-7602-4512-afdb-fb77e44eb50e.jpeg
tags: backend, apis, webdev, 2articles1week, programming-tips

---

Developers who aim to create web applications and APIs using REST should understand the Architecture, Principles and lots more, to build RESTful APIs.

By the end of this tutorial, you will be able to apply this knowledge to your web development projects.

## What is REST?

**REST** stands for **Re**presentational **S**tate **Transfer**, an architectural style that defines a set of constraints and guidelines for creating web services. It simply imposes conditions on how an API should work.

Developers have various architectural styles to design APIs, among which is REST API, which is built following the REST architecture style.

RESTful APIs and REST APIs are often used interchangeably to refer to RESTful web services.

### Key principles:

The REST architectural style has six key principles 💭:

1. **Client-server architecture**: The client and server are separated, and each performs a unique set of functions.
    
2. **Statelessness**: Each client request is independent and stateless, meaning that the server handles each request separately from any previous requests. Clients can request resources in any order without affecting other requests.
    
3. **Cacheability**: RESTful APIs must support caching, which means that responses can be stored and reused later. This significantly improves performance, as the client can avoid making unnecessary requests to the server.
    
4. **Layered system**: The client can function on multiple servers with various layers, including security, application, and logic. These layers work together to respond to client requests without the client having any knowledge of the underlying layers.
    
5. **Uniform interface**: The interface between the client and server must allow the server to transfer information in a standard format. The format of an information representation can differ from its internal server representation. For instance, the server may store data as text but present it in HTML format.
    
6. **Code-on-demand**: The server can provide executable code to the client on demand, such as JavaScript. However, this principle is optional and not always implemented.
    

## What is an API? 🔌

**API** stands for Application Programming Interface. It is a set of rules and protocols that allows different software applications to communicate with each other.

### How does an API work?

APIs act as an intermediary between software applications, enabling them to interact and exchange data, thereby ensuring efficient and effective communication and interaction.

![What is an API (Application Programming Interface)? - GeeksforGeeks](https://media.geeksforgeeks.org/wp-content/uploads/20230216170349/What-is-an-API.png align="left")

Using this real-life example, an API is simply a mediator between clients and servers, similar to how a waiter facilitates communication between customers and the kitchen.

1. Visiting: Customers have to select a restaurant for their desired dishes. Similarly, clients choose a webpage or endpoint to access the resources they need, hoping it offers the required functionality or data.
    
2. Requesting Orders: Customers interact with the waiter by placing their orders, and specifying what dishes they want to have. Similarly, clients interact with an API by sending requests, specifying what resources or actions they need from the server.
    
3. Order Communication: The waiter is like a middleman between customers and the kitchen, relaying their orders. Similarly, an API acts as an intermediary between clients and the server, forwarding requests to the appropriate resources.
    
4. Processing Orders: The kitchen staff receives the orders from the waiter and prepares the requested dishes accordingly. In the API context, the server processes the requests received from the API, performing the necessary actions to retrieve the required data.
    
5. Serving Orders: Once the kitchen has prepared the dishes, the waiter collects them and serves them to the respective customers. In the API context, the server prepares the response based on the client's request and sends it back to the API, which then delivers the response to the client.
    
6. Feedback and Errors: In the restaurant scenario, customers may provide feedback on the served dishes or notify the waiter if something is wrong with their order. Similarly, API responses can include feedback, status codes, or error messages to indicate the success or failure of the request and provide relevant information to the client.
    

### Types of API

APIs come in different types. An understanding of these API types can assist in identifying needs while initiating an API design process.

> While the distinctions between API types can sometimes be unclear, it's important to remember that every API has **an audience scope**, **architecture**, and **protocol**, typically falling into **one** category for each.

For instance, a private API can have either [a monolithic architecture or a microservices architecture](https://www.atlassian.com/microservices/microservices-architecture/microservices-vs-monolith), and it has the flexibility to utilize different protocols based on specific requirements.

**API types by audience:**

* Public APIs
    
* Private APIs
    
* Partner APIs
    

**API types by architecture:**

* [Monolithic APIs](https://www.atlassian.com/microservices/microservices-architecture/microservices-vs-monolith)
    
* [Microservices APIs](https://www.atlassian.com/microservices/microservices-architecture/microservices-vs-monolith)
    
* [Composite APIs](https://aloa.co/startup-glossary-terms/composite-api)
    
* [Unified APIs](https://blog.apideck.com/what-is-a-unified-api)
    

**API types by Protocols:**

* REST APIs
    
* SOAP APIs
    
* GraphQL APIs
    
* RPC APIs
    

## What is RESTful API?

RESTful APIs are simply APIs that adhere to the principles of REST.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684766506248/ab1f3878-a933-4fce-9567-9022ea3a3121.png align="center")

A **RESTful API** is a web service that uses REST resource methods to access and manipulate resources, where each resource is identified [by a unique URI, and not a URL.](https://dev-and-me.hashnode.dev//all-about-rest-principles-restful-apis-authentication-methods/#)

## REST Authentication Methods ✅

Before we proceed, I'd like to address a common misconception regarding the distinction between Authorization and Authentication.

Authorization simply refers to allowing or granting access to a certain action whereas Authentication refers to proving correct Identity - who you say you are.

> *An API might authenticate you but not authorize you to make a certain request.*

Now that we understand authentication, let's explore the most commonly used authentication methods in REST APIs.

Here are common authentication methods used with RESTful APIs:

1. **API Keys:** API keys are unique identifiers issued to clients that grant access to the API. Clients include the API key in their requests to authenticate themselves. API keys are often used for public APIs or when authentication needs to be simple and lightweight.
    
2. **OAuth**: OAuth is an authorization framework that enables delegated access to an API on behalf of a user. It allows users to grant permissions to third-party applications without sharing their login credentials. OAuth involves the exchange of access tokens to authenticate and authorize API requests.
    
3. **Token-Based Authentication**: Token-based authentication involves exchanging credentials for a token that is sent with subsequent requests. The token can be stored client-side and sent in the Authorization header or as a query parameter. An example is **JSON Web Tokens (JWT).**
    
4. **Basic Authentication**: Basic Authentication involves sending the username and password in the request headers encoded. However, it is considered less secure than other authentication methods, as the credentials are sent with each request in plain text.
    
5. **Single Sign-On (SSO):** SSO allows users to log in once and gain access to multiple systems or applications. The API can leverage SSO protocols like SAML (Security Assertion Markup Language) or OpenID Connect to authenticate users and authorize their access.
    

It's important to choose an appropriate authentication method based on your API's security requirements and the sensitivity of the data being accessed.

Some APIs may require a combination of multiple authentication layers. For Instance, combining API keys with OAuth or JWT for enhanced security.

## What is a REST Resource?👀

A REST resource refers to any piece of information that can be identified and manipulated through a unique identifier. it can be a user, a document, an image or a non-virtual object.

In REST, every resource possesses a distinct URI, and the interactions with that resource are dictated by the HTTP methods. This is referred to as **resource representation.**

The resource representations in REST consist of three main components:

1. **Data**: This refers to the actual information contained within the resource. The API's design allows for flexibility as it is not constrained to a specific data format. It can be structured data in various formats such as JSON, XML, or HTML.
    
2. **Metadata:** Metadata provides additional information about the resource. It includes details such as the resource's creation date, last modification timestamp, author, format, or any other relevant information that helps in understanding and managing the resource.
    
3. **Hypermedia Links**: Hypermedia links are links embedded within the resource representation and serve as navigational cues, providing discoverable links for clients. With these links, clients can dynamically explore the API, interacting with related resources.
    

Together, these components provide a comprehensive package, enabling clients to understand and manipulate the API's resources effectively.

### Resource Methods 🤷

In connection with RESTful APIs, resource methods refer to the actions or operations that can be performed on a particular resource. There 4 primary methods associated with the standard HTTP verbs providing a standardized way to perform basic CRUD operations on resources.

| **Method** | **Description** |
| --- | --- |
| GET | Retrieve information about the REST API resource |
| POST | Create a REST API resource |
| PUT | Update a REST API resource |
| DELETE | Delete a REST API resource or related component |

Additionally, RESTful APIs can also support other custom methods to perform specific actions on resources beyond the basic CRUD operations, based on the application's requirements.

## REST !== HTTP 🤔

When discussing REST, it's natural to associate it with HTTP (Hypertext Transfer Protocol).

HTTP and REST are closely connected but have distinct purposes.

HTTP is a widely adopted standard with clear constraints. It serves as a communication protocol that powers most of our everyday internet interactions.

In contrast, REST is not a standard or specification in itself, but rather an architectural style. It offers guidance on how to structure APIs and organize resources to enhance communication efficiency.

it's important to note that not all HTTP interactions are RESTful. While HTTP possesses the necessary features of a RESTful system, it is not always considered RESTful.

## Summary 💥

Understanding the principles, architecture, authentication methods, resource handling, and the relationship between REST and HTTP is crucial for developers looking to create web applications and APIs using REST.

Applying this knowledge aids the development of efficient, scalable, and interoperable RESTful APIs for their web development projects.

My next article will be on the implementation of RESTful APIs, building with Express and MySQL as database management systems.

Thanks for reading ✅ You can connect with me on [**Twitter**](https://twitter.com/geoan_g) and [**LinkedIn**](https://www.linkedin.com/in/georgeangel1/).

## Resources

👉 [Best practices for naming REST API endpoints](https://blog.dreamfactory.com/best-practices-for-naming-rest-api-endpoints/)

👉 [Best practices for REST API design](https://stackoverflow.blog/2020/03/02/best-practices-for-rest-api-design/)

👉 [HTTP Methods](https://restfulapi.net/http-methods/)

👉 [HTTP status codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)

👉 [REST vs gRPC - what's the difference? 🤔](https://amplication.com/blog/rest-vs-grpc-whats-the-difference)

👉 [SOAP vs REST vs GraphQL](https://javascript.plainenglish.io/soap-vs-rest-vs-graphql-difference-between-web-api-services-461eee5d1ad7)