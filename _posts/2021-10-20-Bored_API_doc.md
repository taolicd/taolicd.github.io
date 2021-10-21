---
layout: post
title: "Bored API Quickstart Guide to the Bored API"
date: 2021-10-20
categories: REST APIs
---

## What is the Bored API for

The [Bored API](www.boredapi.com) is a web API for submitting queries to find things to do to kill boredom. 


## Authentication 
You do not need an API key to use this API. Just submit a query to the endpoint `/api/activity/` to retrieve a suggested activity. 


## Installation and deployment 

The API was built using  [MEVN stack](https://www.educative.io/edpresso/what-is-mevn-stack) with Frontend using Vue.js and Webpack and Backend using Node.js and MongoDB. The application on [www.boredapi.com](www.boredapi.com) is hosted on Heroku. You can use this hosted API for querying activities. You can also install and deploy your own service. 

To install and deploy this project on your own machine:
1. Install Node.js and MongoDB.
2. Clone the project from https://github.com/drewthoennes/Bored-API.
3. Start MongoDB instance, change directory to the clone project and run

```
npm install
npm start
```
4. The application is started on https://hostname/8080


## Endpoint definitions

See [Bored swagger UI](https://taolicd.github.io/swagger-for-bored-api/) for details. The Swagger UI is hosted under Tao's personal GitHub Pages. 

## Example responses

The Get response is in JSON format.

```
{ "activity": "Learn how the internet works",
  "type": "education",
  "participants": 1,
  "price": 0,
  "link": "",
  "key": "9414706",
  "accessibility": 0.1
}

```



## Use cases

The Bored API has been used in other applications and projects such as 

* [I'm Bored Alexa skill](https://www.amazon.com/gp/product/B07GDL9MP4?ie=UTF8&ref-suffix=ss_rw)
* [Python wrapper](https://pypi.org/project/bored/)
* [Kotlin wrapper](https://gitlab.com/CMDR_Tvis/bored-api)
* [React app](https://github.com/CDAracena/Im-Bored)
* [Vue app](https://github.com/emilsgulbis/BoredApp)
* [iOS app](https://apps.apple.com/us/app/bored-find-what-to-do/id1475656469)



### Future feature suggestions

* Add API authentication. This will be useful if we decide to support POST, DELETE, UPDATE operations in the future.
*
*
Currently the only action supported is GET. 


### Known issues

Error code is not standardized. 

### Suggestions for changes

The `accessibility` parameter probably should be changed to a easier and clearer word such as `difficulty`. 








