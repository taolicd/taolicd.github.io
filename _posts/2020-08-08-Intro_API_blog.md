---
layout: post
title:  "A Beginner's Guide to APIs"
date:   2020-08-08
categories:  REST API

---
# A Beginner's Guide to APIs 


## What is an API 

Nowadays we are bombarded with the term API. What is an API anyway? 

API stands for Application Programming Interface. It defines a set of protocols and rules to allow software applications to interact with each other. 

For example, you have a Facebook account and you just downloaded Yelp on your mobile. When registering with Yelp, you are presented with the option to log in using your Facebook account. If you choose to log in with your Facebook account, you authorize Facebook's API to access your Facebook login account and use it for your Yelp login. The benefit to you is you have one less login account to remember.  The benefit to Yelp is it may further ask you to grant permission to access your Facebook friends. 


## Authentication and authorization 

Because APIs use data and services from other applications, it is important that only authorized users or accounts are allowed into the applications. Typically this process involves two steps: 

 1. Authentication: Authentication means you need to prove you are who you are. 

 2. Authorization: Authorization means the API is authorized (granted permission) to access the data and services on another application. 

In the example of using Facebook account to log into Yelp, first you are directed to your Facebook login and asked for your Facebook credential. This is the authentication step. After the authentication is successful, you are asked whether you authorize Yelp to use your Facebook login. Upon confirmation, you are logged in using your Facebook credential and redirected to Yelp.

Each software vendor has its own portal to grant users access to its API services and monitor API usages. Typically API assumers[^1] need to pay for accessing private data and services. Think of this transaction as checking in a hotel. You pay an agreed fee and you get a hotel room key, which allows you have access to the room and amenities for a certain period based on agreed upon conditions. 

There are several API authorization methods. The most common ones are API keys and OAuth. Some APIs support multiple authorization methods. 

### What is an API key and where to get one

An API key is a token that consists of a string of random looking characters. With this token, you are granted access to certain data and services. To get an API key, you need to register with individual software vendors. For example, Google's popular [geocode](https://developers.google.com/maps/documentation/geolocation/intro) API allows you to access Google's geolocation data. You can register with Google Cloud Platform and get an API key from [Google](https://developers.google.com/maps/documentation/geolocation/get-api-key). For non frequent users, the service is free. If your app needs to call for services more than a certain times a day, you pay a fee. 

###  What is OAuth and where to get one

Another popular authorization tool is called [OAuth](https://en.wikipedia.org/wiki/OAuth). OAuth has version 1.0 and 2.0. OAuth version 1.0 is now obsolete and OAuth version 2.0 is widely adopted. To set up OAuth2 authorization, register as a developer with individual vendors. For example, for accessing twitter data via its APIs using its OAuth, you need to register as a [twitter developer](https://developer.twitter.com/en/docs/authentication/overview). For setting up OAuth2 with Google, see [Using OAuth 2.0 to Access Google APIs](https://developers.google.com/identity/protocols/oauth2). 

### Public APIs 

Some APIs do not need authorization. Some require authorization but do not charge you for accessing the data and services. These are public APIs that give you access to public data and services. Think of public APIs that do not need authorization as parks where people have unrestricted access. They are open to everyone and free. Think of public APIs that require authorization as public libraries. They are open to everyone but you need to register to borrow books. 

Here is a collection of interesting public APIs [https://github.com/public-apis/public-apis](https://github.com/public-apis/public-apis). On this page, the Auth column identifies whether authorization is required for using the corresponding API. 


##  What can you use APIs for

Web developers and app developers are the obvious consumers and creators of APIs. For example, a web developer may embed a Google map  on her website using Google's geolocation API. Yelp using Facebook login also belongs to this category. To the end user who browses the website with a Google map or the Yelp user who logs in using Facebook account, this type of API usage is software to software and invisible to users. 

APIs are also heavily used by people with or without any programming experiences. Recently more people are using a special type of web APIs called REST APIs. REST stands for Representational State Transfer. When used in the context of web, REST APIs take advantage of the HTTP protocol, which is the protocol for web browsing. This makes things very convenient because you can just use a web browser to send API requests. This type of API usage is human to software and the results are returned to the human requesters. This use case is very popular among web scraping enthusiasts and data scientists. Web scraping is a technique for gathering information from websites. Data scientists are people who analyze data to gain underlying insights that are not obvious to ordinary people. By using REST APIs, web scrapers and data scientists can get large amount of interesting raw data from the web. 

## REST API syntax

A REST API mainly contains three parts: 

* Resource (noun)
* Method (verb)
* Parameters

**Resources** as nouns. They are the things you want to work with, such as a book, a post, a user, or an account. 

**Methods** are verbs/actions you want to perform on your resources (i.e. nouns). 
The most common HTTP methods/verbs include:

* GET: retrieve a resource
* POST: create a new resource
* PUT: update or replace an existing resource
* DELETE: delete a resource 

**Parameters** specify the conditions you need to complete the action/method. For example, when you use Google to search for a keyword, you are providing the keyword as the parameter and using the GET method to retrieve the relevant resources from the web. GET is the most frequently used method. This is because the majority of web users only retrieve information from the web rather than updating or deleting anything. Some parameters are mandatory, which means if you don't specify them, the API will not work. Different APIs have different rules. Refer to the each vendor's API documentation for details. 

Another important factor to keep in mind is, to perform actions such as POST, PUT and DELETE, most likely you need authorization. This means you need an API key or use OAuth to do these actions. Even the GET method is not always publicly available in many REST APIs. You need to register with the API providers to get authorization. For example, if you want to get data from New York Times, you need to get a New York Times Developer account so you can work with their APIs. 

In this example REST API syntax, the API key is submitted as part of the parameters:

```
{Method} 
http(s)://{domain/resources}?
{param1=value1&param2=value2&...&api_key=your_api_key}
```
in which

* Methods are typically one of the following: GET, POST, PUT, DELETE.
* `domain/resources` is the resource you are trying to retrieve, create, update, or delete. 
*  param-value pairs and API_key and value pair specify the actual parameters used for this API request. 
* `?` is a symbol to indicate the end of the resource specification and the beginning of the parameters. 
* `&` specifies the "and" condition in the parameters.
 
Here is an example using Google's Book API for retrieving book info based on an ISBN number. It contains three parts. No API key is needed in this case because the data is public. 

* method: `GET`
* resource: `wwww.googleapis.com/books/v1/volumes`
* parameters: `q=isbn:0747532699`, which indicates I am querying for info on a book with the isbn number 0747532699
   
```
GET https://www.googleapis.com/books/v1/volumes?q=isbn:0747532699
```

Tip: The GET method is the default method in a web browser, which is why when you browse a website, you just need to type the URL (universal resource locator) and the optional parameters and do not need to include the Get keyword. 


### Chrome Postman

To try how REST API works, you can install a handy Chrome plugin called Postman. The Postman plugin is a tool for you to learn and test REST API requests. 


## Where to find interesting APIs

A good place to explore the available web APIs is [programmableweb](http://www.programmableweb.com/apis/directory). The opportunities are endless. Have fun!


[^1]:
In the case of Yelp using your Facebook login, you don't need to worry about Facebook charging you for using the API usage. If there is any payment, it is between Yelp and Facebook.
