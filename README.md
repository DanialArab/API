# APIs

This repo documents my understandings of APIs. Here is the structure of my notes. 

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
### Web APIs (HTTP-based APIs):

<a name="5"></a>
#### RESTful APIs (Representational State Transfer)

These are the most common type of web APIs, which adhere to a set of architectural constraints and principles. They use standard HTTP methods (GET, POST, PUT, DELETE) to perform CRUD operations on resources.

<a name="6"></a>
#### SOAP APIs (Simple Object Access Protocol)

These APIs use XML-based messages and typically run over HTTP, SMTP, TCP, or other transport protocols. They have more rigid specifications and use XML schemas for data exchange.

<a name="7"></a>
### Library APIs (SDKs):

Library APIs provide a set of functions or classes within a programming language that developers can use to access the features of a particular library or software development kit (SDK).

<a name="8"></a>
### Operating System APIs:

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





