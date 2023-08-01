# APIs

This repo documents my understanding of APIs. Here is the structure of my notes.  

1. [Introduction](#1)
   1. [Web scraping vs. API calls](#2)
   1. [Types of APIs](#3)
      1. [Web APIs (HTTP-based APIs)](#4)
         1. [RESTful APIs (Representational State Transfer)](#5)
         2. [SOAP APIs (Simple Object Access Protocol)](#6)
      2. [Library APIs (SDKs)](#7)
      3. [Operating System APIs](#8)
      4. [Hardware APIs](#9)
      5. [Database APIs](#10)
      6. [Remote APIs](#11)
      7. [Webhooks](#12)
      8. [Open APIs (Public APIs)](#13)
      9. [Internal/Private APIs](#14)
      10. [Third-party API](#15)
2. [RESTful APIs](#16)
   1. [Intro to JSON](#17)
   2. [Request Methods](#18)
      1. [HTTP GET](#19)
      2. [HTTP POST](#20)
      3. [HTTP DELETE](#21)
      4. [HTTP PUT](#22)
      5. [HTTP PATCH](#23)
   3. [Consuming APIs (how to use them)](#24)
   4. [Requests and Responses](#25)
   5. [Common HTTP Status Code](#26)
      1. [Healthy Responses (2--)](#27)
      2. [Redirect Responses (3--)](#28)
      3. [Client Responses (4--)](#29)
      4. [Server Responses (5--)](#30)
    6. [API Security](#31)
       1. [API Keys](#32)
3. [Reference](#33)



<a name="1"></a>
## Introduction

<a name="2"></a>
### Web scraping vs. API calls

Web scraping and API calls are two different ways to retrieve data from websites, with some key differences in terms of their implementation and usage.

#### Web Scraping:

Web scraping involves extracting data from websites by parsing the **HTML or XML code of web pages.** This is typically done using a web scraping tool or library, such as **BeautifulSoup** or **Scrapy**, that can parse the HTML code and extract the data of interest. Web scraping can be useful for **extracting data from websites that don't have an API or for retrieving data that is not available through an API**. However, **web scraping can also be more complex and time-consuming than using an API**, as it requires parsing HTML code and handling various website structures and layouts. Web scraping may be illegal or unethical in some cases, as it can violate website terms of service or infringe on copyright or privacy rights.
    
#### API Calls:

API calls, on the other hand, involve retrieving data from a web API service by **making HTTP requests to the API endpoint**. **APIs provide a structured and standardized way for applications to exchange data with each other over the Internet.** APIs typically provide **data in a structured format, such as JSON or XML, that can be easily processed by applications.** Using an API can be simpler and more efficient than web scraping, as the data is provided in a structured and standardized format, and there are typically fewer website structures and layouts to handle.

In summary, web scraping and API calls are two different methods for retrieving data from websites, with different advantages and disadvantages. Web scraping can be more flexible and powerful but also more complex and time-consuming, while API calls are typically simpler and more efficient but require a web API service to be available.

<a name="3"></a>
### Types of APIs 

APIs (Application Programming Interfaces) can be categorized into several types based on their **functionality, usage, and the way they are implemented**. But **RESTful APIs** are most commonly talked about these days. It doesn’t matter what programming language we’re using. JavaScript, Python, PHP, Java, C and every other modern language supports RESTful APIs. Here are some common types of APIs:

<a name="4"></a>
### Web APIs (HTTP-based APIs)

<a name="5"></a>
#### RESTful APIs (Representational State Transfer)

These are the most common type of web APIs, which adhere to a set of architectural constraints and principles. They use standard HTTP methods (GET, POST, PUT, DELETE) to perform CRUD operations on resources.

<a name="6"></a>
#### SOAP APIs (Simple Object Access Protocol)

These APIs use XML-based messages and typically run over HTTP, SMTP, TCP, or other transport protocols. They have more rigid specifications and use XML schemas for data exchange.

<a name="7"></a>
### Library APIs (SDKs)

Library APIs provide a set of functions or classes within a programming language that developers can use to access the features of a particular library or software development kit (SDK).

<a name="8"></a>
### Operating System APIs

Operating System APIs expose functionalities provided by the operating system to developers. For example, the Windows API or POSIX API allow developers to interact with the underlying OS services like file management, networking, and process management.

<a name="9"></a>
### Hardware APIs

These APIs provide access to hardware features and functionalities of a device. Examples include APIs for accessing the camera, sensors, GPS, etc., on a mobile phone.

<a name="10"></a>
### Database APIs

Database APIs allow applications to interact with databases. Examples include the Python DB-API for accessing databases from Python code.

<a name="11"></a>
### Remote APIs

Remote APIs enable communication and interaction between applications or services across a network. These can be web-based APIs or other forms of remote communication like Remote Procedure Call (RPC).

<a name="12"></a>
### Webhooks

Webhooks are a form of API where an application can provide a URL to another application, and the second application will send HTTP requests to that URL whenever certain events occur.

<a name="13"></a>
### Open APIs (Public APIs)

Open APIs are publicly available APIs that are open to developers outside the organization that owns the API. They allow third-party developers to access and use the API's functionalities to build applications and services.

<a name="14"></a>
### Internal/Private APIs

Internal APIs are meant for internal use within an organization. They are not exposed to the public and are used to enable communication between different services or components of the organization's infrastructure.

<a name="15"></a>
### Third-party APIs

These are APIs provided by external organizations or services, which developers can use to access specific functionalities or data from those services. Examples include social media APIs (Facebook, Twitter), payment gateways (PayPal, Stripe), and more.

Each type of API serves a specific purpose and plays a crucial role in modern software development by enabling integration, interoperability, and extensibility between different applications and services.


<a name="16"></a>
## RESTfull APIs

Simply put, a client computer asks another computer for data, or to take an action to modify, delete, or create data.

<a name="17"></a>
### Intro to JSON

When we make a standard RESTful API request to a service, it gives us a response back in the form of JSON, which is a structured key-value pair.

<a name="18"></a>
### Request Methods

<a href="https://restfulapi.net/http-methods/">http request methodsI</a>

<a name="19"></a>
#### HTTP GET

+ When we load a website. That’s a GET request
+ It’s a request to get data from another computer
+ We’re simply asking for data and we’re not asking to perform a task
+ We’re not creating, updating, or deleting data
+ It is the most common request type
+ Its CRUD (Create, Read, Update, Delete) operation is Read
+ Example URL(s): http://website.com/api/users/ OR http://website.com/api/user/1/


<a name="20"></a>
#### HTTP POST

+ They do not go through the standard URL, but use a URL as the endpoint
+ Ask another computer to create a new resource
+ Returns data about the newly created resource
+ Its CRUD operation is Create
+ An example would be when a new user tries to sign up in Facebook 
+ Example URL(s): http://website.com/api/users/

<a name="21"></a>
#### HTTP DELETE

+ Do not go through the standard URL, but use a URL as the endpoint
+ Ask another computer to delete a single resource or a list of resources
+ Use it with caution
+ Its CRUD operation is Delete 
+ An example would be when you would like to delete your credit card info from your Amazon account or delete an image from your Facebook profile
+ Example URL(s): http://website.com/api/user/1/

<a name="22"></a>
#### HTTP PUT

+ They do not go through the standard URL, but use a URL as the endpoint
+ Ask another computer to update an **entire resource**
+ If the resource doesn’t exist, some of the APIs might decide to CREATE (CRUD) the resource
+ Its CRUD operation is Update/Replace 
+ Example URL(s): http://website.com/api/user/1/

<a name="23"></a>
#### HTTP PATCH	

+ They do not go through the standard URL, but use a URL as the endpoint
+ Ask another computer to update a **piece of a resource**
+ They are not fully supported by all browsers or frameworks (like Django), so we typically fall back on PUT requests
+ Since PATCH is not supported in a lot of different areas, we rely on PUT instead 
+ Example: Updating a user's first name
+ Its CRUD operation is a partial Update/Modify
+ Example URL(s): http://website.com/api/user/1/firstname/

<a name="24"></a>
### Consuming APIs (how to use them) 

+ APIs can be written in almost any server-side (back-end) language as long as that language accepts HTTP protocol requests such as GET, POST, DELETE, PUT
+ When a client (such as a web browser) makes an API request to a website or a web application, the server-side code processes the request, interacts with databases, performs calculations, and generates the appropriate content to be sent back to the client. APIs will generally return  one of two types data structures: **JSON** or **XML**
+ XML gives the exact same stuff back as JSON but it just looks different. JSON is a bit more lightweight, flexible, and robust. A nice thing about XML though is that it comes with a contract, which generally means that the type of the data (corresponding to the values in JSON key-value pairs) should always be specified like to be an integer/string/etc.
+ APIs can be consumed in almost any language: Browsers use JavaScript for their API requests, while Servers use any language that runs on that computer.

<a name="25"></a>
### Requests and Responses 

+ When we request data from a server using GET, POST, PUT, PATCH or DELETE… that’s a request. 
+ When the server returns our data… that’s a response
+ Responses will always come with an **HTTP Status Code**. And these “status codes” tell us what’s **wrong (or right) without needing to give us text back to read.**

<a name="26"></a>
#### Common HTTP Status Codes

<a href="https://www.webfx.com/web-development/glossary/http-status-codes/">HTTP Status Codes Glossary</a>

<a name="27"></a>
##### Healthy Responses (2--)
+ 200 — OK. Request accepted.
+ 201 — Created. POST requests often return 201s when a resource is created.
+ 202  — Accepted. When a request is accepted but it is not done processing. Maybe the task goes into a queue.


<a name="28"></a>
##### Redirect Responses (3--)

+ 301 — Moved Permanently.  When the endpoint has permanently changed. Update your endpoint. 
+ 302 — Found.  The endpoint you’re accessing is temporarily moved to somewhere else.

<a name="29"></a>
##### Client Responses (4--)

+ 400 — Bad Request. The server cannot or will not process your request. Often this is due to malformed API keys or an invalid payload. 
+ 401 — Unauthorized.  You’re not allowed here. Usually, this is because you’re missing authentication credentials (API keys)
+ 403 — Forbidden.  The servers understand your request but won’t execute it. Your API keys might not have the right permissions or you are trying to use an endpoint that you don’t have access to.
+ 404 — Not Found.  There’s nothing here. Move along, move along.
+ 405 — Method Not Allowed.  You’re using the wrong HTTP Method. The endpoint might only accept GET requests and you might be POSTing to it, for example.

<a name="30"></a>
##### Server Responses (5--)

+ 500 — Internal Server Error. The server had a problem and couldn’t process the request. This is the only time you are out of control. You did not do anything to break it and so you cannot do anything about it. 

<a name="31"></a>
#### API Security

<a name="32"></a>
##### API Keys

+ API keys are “passwords” to access an API. These are your authentication credentials.
+ Almost every website requires API keys to perform some action.
+ Facebook's Graph API is a good example: graph.facebook.com/codingforeverybody

<a name="33"></a>
### Reference

<a href="https://www.udemy.com/course/learn-and-understand-apis-and-restful-apis/?utm_source=adwords&utm_medium=udemyads&utm_campaign=Webindex_Catchall_la.EN_cc.CA&utm_term=_._ag_119831896715_._ad_533102824797_._kw__._de_c_._dm__._pl__._ti_dsa-391662294458_._li_9001493_._pd__._&matchtype=&gclid=Cj0KCQjw2qKmBhCfARIsAFy8buISk-i0ysapCg5aDv5pni2DU3nu_4RQJ6kIBaKDqQflbbCUwG1GKLYaAtbkEALw_wcB">Understanding APIs and RESTful APIs Crash Course</a>



