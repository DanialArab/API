# API

This repo documents my understandings of APIs. Here is the structure of my notes. 

1. [Introduction](#1)
   1. [Types of APIs](#2)
      1. [Web APIs (HTTP-based APIs)](#3)
         1. [RESTful APIs (Representational State Transfer)](#4)
         2. [SOAP APIs (Simple Object Access Protocol)](#5)
      2. [Library APIs (SDKs)](#6)
      3. [Operating System APIs](#7)
      4. [Hardware APIs](#8)
      5. [Database APIs](#9)
      6. [Remote APIs](#10)
      7. [Webhooks](#11)
      8. [Open APIs (Public APIs)](#12)
      9. [Internal/Private APIs](#13)
      10. [Third-party API](#14)


<a name="1"></a>
## Introduction

APIs (Application Programming Interfaces) can be categorized into several types based on their **functionality, usage, and the way they are implemented**. Here are some common types of APIs:

<a name="2"></a>
### Types of APIs 

<a name="3"></a>
### Web APIs (HTTP-based APIs):

<a name="4"></a>
#### RESTful APIs (Representational State Transfer)

These are the most common type of web APIs, which adhere to a set of architectural constraints and principles. They use standard HTTP methods (GET, POST, PUT, DELETE) to perform CRUD operations on resources.

<a name="5"></a>
#### SOAP APIs (Simple Object Access Protocol)

These APIs use XML-based messages and typically run over HTTP, SMTP, TCP, or other transport protocols. They have more rigid specifications and use XML schemas for data exchange.

<a name="6"></a>
### Library APIs (SDKs):

Library APIs provide a set of functions or classes within a programming language that developers can use to access the features of a particular library or software development kit (SDK).

<a name="7"></a>
### Operating System APIs:

Operating System APIs expose functionalities provided by the operating system to developers. For example, the Windows API or POSIX API allow developers to interact with the underlying OS services like file management, networking, and process management.

<a name="8"></a>
### Hardware APIs

These APIs provide access to hardware features and functionalities of a device. Examples include APIs for accessing the camera, sensors, GPS, etc., on a mobile phone.

<a name="9"></a>
### Database APIs

Database APIs allow applications to interact with databases. Examples include the Python DB-API for accessing databases from Python code.

<a name="10"></a>
### Remote APIs

Remote APIs enable communication and interaction between applications or services across a network. These can be web-based APIs or other forms of remote communication like Remote Procedure Call (RPC).

<a name="11"></a>
### Webhooks

Webhooks are a form of API where an application can provide a URL to another application, and the second application will send HTTP requests to that URL whenever certain events occur.

<a name="12"></a>
### Open APIs (Public APIs)

Open APIs are publicly available APIs that are open to developers outside the organization that owns the API. They allow third-party developers to access and use the API's functionalities to build applications and services.

<a name="13"></a>
### Internal/Private APIs

Internal APIs are meant for internal use within an organization. They are not exposed to the public and are used to enable communication between different services or components of the organization's infrastructure.

<a name="14"></a>
### Third-party APIs

These are APIs provided by external organizations or services, which developers can use to access specific functionalities or data from those services. Examples include social media APIs (Facebook, Twitter), payment gateways (PayPal, Stripe), and more.

Each type of API serves a specific purpose and plays a crucial role in modern software development by enabling integration, interoperability, and extensibility between different applications and services.

