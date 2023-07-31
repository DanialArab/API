# API

This repo documents my understandings of APIs. Here is the structure of my notes. 

1. [Introduction](#1)
   1. [Web APIs (HTTP-based APIs)](#2)
      1. [RESTful APIs (Representational State Transfer)](#3)
      2. [SOAP APIs (Simple Object Access Protocol)](#4)


<a name="1"></a>
## Introduction

APIs (Application Programming Interfaces) can be categorized into several types based on their **functionality, usage, and the way they are implemented**. Here are some common types of APIs:

<a name="2"></a>
### Web APIs (HTTP-based APIs):

<a name="3"></a>
#### RESTful APIs (Representational State Transfer)

These are the most common type of web APIs, which adhere to a set of architectural constraints and principles. They use standard HTTP methods (GET, POST, PUT, DELETE) to perform CRUD operations on resources.

<a name="4"></a>
#### SOAP APIs (Simple Object Access Protocol)

These APIs use XML-based messages and typically run over HTTP, SMTP, TCP, or other transport protocols. They have more rigid specifications and use XML schemas for data exchange.
Library APIs (SDKs):

Library APIs provide a set of functions or classes within a programming language that developers can use to access the features of a particular library or software development kit (SDK).
Operating System APIs:

Operating System APIs expose functionalities provided by the operating system to developers. For example, the Windows API or POSIX API allow developers to interact with the underlying OS services like file management, networking, and process management.
Hardware APIs:

These APIs provide access to hardware features and functionalities of a device. Examples include APIs for accessing the camera, sensors, GPS, etc., on a mobile phone.
Database APIs:

Database APIs allow applications to interact with databases. Examples include the Python DB-API for accessing databases from Python code.
Remote APIs:

Remote APIs enable communication and interaction between applications or services across a network. These can be web-based APIs or other forms of remote communication like Remote Procedure Call (RPC).
Webhooks:

Webhooks are a form of API where an application can provide a URL to another application, and the second application will send HTTP requests to that URL whenever certain events occur.
Open APIs (Public APIs):

Open APIs are publicly available APIs that are open to developers outside the organization that owns the API. They allow third-party developers to access and use the API's functionalities to build applications and services.
Internal/Private APIs:

Internal APIs are meant for internal use within an organization. They are not exposed to the public and are used to enable communication between different services or components of the organization's infrastructure.
Third-party APIs:

These are APIs provided by external organizations or services, which developers can use to access specific functionalities or data from those services. Examples include social media APIs (Facebook, Twitter), payment gateways (PayPal, Stripe), and more.
Each type of API serves a specific purpose and plays a crucial role in modern software development by enabling integration, interoperability, and extensibility between different applications and services.
