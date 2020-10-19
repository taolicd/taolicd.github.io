---
layout: post
title:  "A Beginner's Guide to APIs"
date:   2019-08-08
categories:  API, REST

---
# A Beginner's Guide to APIs 


## What is an API 

Nowadays we are bombarded with the term API. What is an API anyway? 

API stands for Application Programming Interface. It defines a set of protocols and rules to allow software applications to interact with each other. People use APIs to build applications by connecting to other applications and using data and services that are inside other applications. For example, you have a Facebook account and you just downloaded Yelp on your mobile. When registering with Yelp, you are presented with the option to create a new Yelp account or log in using your Facebook account. If you choose to log in with your Facebook account, you authorize Yelp's API to access your Facebook login account and use it for your Yelp login. The benefit to you is now there is one less login account to remember.  The benefit to the vendor (in this case Yelp) is it can ask you to grant permission to access your Facebook friends. 


## Authentication and authorization 

Because APIs use data and services from other applications, it is important that only authorized users are allowed into the applications. This stage involves two steps: 

 1. Authentication: Authenticaiton means you need to prove you are who you are and you are allowed to access the data and services. 

 2. Authorization: Authorization means you authorize the API to access your data on another application. 

In the example of using Facebook account to log in to Yelp, first you will be directed to your Facebook login and you will be asked for your Facebook login credential. This is the authentication step. After the authenfication is successful, you will be asked whether you authorize Yelp to access to your Facebook login. After your confirmation, you will then be redirected back to Yelp.

APIs can bring revenue because companies may charge API assumers for accessing their private data and resources. Companies set up mechanisms to manage and monitor API usage of their data and resources and require API assumers[^1] to pay certain amount of fees for their data and services. Think of this as if you check in a hotel. If you pay an agreed fee, you get the hotel room key, which allows you have access to the room and amendities for a certain period based on agreed upon conditions. 

There are several API authorization methods. The most common ones are API keys and OAuth. Some APIs support both methods and some support one but not the other. 

### What is an API key and where to get one?

An API key is a string of random looking characters that grants you access to private data and services. To get an API key, you need to register with individual vendors. For example, Google's popular [geocode](https://developers.google.com/maps/documentation/geolocation/intro) API allows you to access Google's geolocation data. You can register with Google Cloud Platform and get an API key from [Google](https://developers.google.com/maps/documentation/geolocation/get-api-key). For non frequent users, the service is free. If the app needs to call for services more than a certain times a day, you pay a fee. 

###  What is OAuth and where to get one? 

Another popular authorization tool is called [OAuth](https://en.wikipedia.org/wiki/OAuth). OAuth has version 1.0 and 2.0. OAuth version 1.0 is now obsolete and OAuth version 2.0 is widely adopted. To set up OAuth2 authorization, register as a developer wtih indiviual vendors. For example, for accessing twitter data via its APIs, you can register as a [twitter developer](https://developer.twitter.com/en/docs/authentication/overview). For setting up OAuth2 with Google, see [Using OAuth 2.0 to Access Google APIs](https://developers.google.com/identity/protocols/oauth2). 

### Public APIs that do not need authorization

Some public APIs do not need API keys or OAuth. These APIs give you access to public data and services. Think of public APIs as public libaries. They are open to everyone and free. 

For example, there is a public API called [numbersapi](http://numbersapi.com/)
on numbers. If you click [this link](http://numbersapi.com/1..100), you will get facts on numbers from 1 to 100. This is because in the URL above, I put 1..100 as the parameter for this API query. If you change the parameter, the return results will be different. I will explain REST API syntax. 


Another example is Google's Book API, which allows you to get/search public data for books based on ISBN without authentication. Take a close look at the isbn in the URL below. You can change the ISBN number to get results from a different book. 
[Google free REST API for book search based on isbn](https://www.googleapis.com/books/v1/volumes?q=isbn:0747532699)

Here is [a galary of public APIs](https://github.com/public-apis/public-apis).

##  What can ordinary users use APIs for?

Web developers and app developers are the obvious consumers and creators of web APIs. Using APIs provided by other companies, web developers and app developers can gain access to data and resources previously not available to them. They can also open up their own data and resources by creating APIs for others to use. APIs usually come with API documentation to help users . 


Another big user group of APIs are web scraping enthusiasts and data scientists. Web scraping is a technique for gathering information from websites. Data scientists are people who analyze data to gain underlying insights that are not obvious to ordinary people. By using APIs, web scrapers and data scientists can get large amount of interesting raw data from the web in batch mode. 


To perform actions such as POST, PUT and DELETE, most likely you will need permission/authorization. This means you need an API key to do those actions. Even the GET method is not always publicly available in many REST APIs. You need to register with them to get the API key. An API key can be submitted as part of the parameters. 


For example, the Google API for retrieving book info based on ISBN number contains the following three parts: 

* method: `GET`
* resource: `wwww.googleapis.com/books/v1/volumes`
* parameters: `q=isbn:0747532699`, which indicates I am querying for info on a book with the isbn number 0747532699
   
```
GET https://www.googleapis.com/books/v1/volumes?q=isbn:0747532699
```

Note: In a web browser, the GET method is the default method, which means you do not need to include the Get method in a web browser.


## Chrome Postman

To try out how API works, a handy plugin you can install is Chrome's Postman. See [Postman](https://www.getpostman.com/) for details. 

Click this 
[link](https://github.com/taolicd/taolicd.github.io/tree/master/images/postmannew.jpeg) to view a screen shot of the Postman GUI. 



## Using REST APIs to gather data for data analysis and data aggregation

So now you know that you can get raw data in JSON or XML from your favorite websites such as Yelp, Twitter, Facebook or New York Times. 

The Postman plugin is a tool for you to learn and test API calls. In real life  scenarios, you probably will write some sort of scripts to automate the web scraping activity. A good tool to start with is the [curl](https://en.wikipedia.org/wiki/CURL). 

The next task is to try to make sense of the raw data and find patterns. This is out of the scope for today's discussion. 


## Where to find interesting web APIs?

A good place to explore the available web APIs is [programmableweb](http://www.programmableweb.com/apis/directory). The opportunities are endless. Have fun!


[^1]:
In the case of Yelp using your Facebook login, you don't need to worry about Facebook charging you anything for using the Yelp API. If there is any moneytary transaction, it is between Yelp and Facebook, not you.
