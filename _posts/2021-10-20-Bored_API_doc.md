---
layout: post
title: "Bored API Quickstart Guide"
date: 2021-10-20
categories: REST APIs
---

# Quickstart Guide to the Bored API



## What is the Bored API

The Bored API is a web application for submitting queries to find things to do when you need to kill boredom. 


## Authentication 
You do not need an API key to use this API. Just submit a query to the endpoint /api/activity/ to retrieve a suggested activity. 


## Installation, configuration and deployment 

The API was built using  MEVN stack (MongoDB, Express.js, Vue.js, and Node.js) with frontend using Vue.js and Webpack and backend using Node.js and MongoDB. The application on [www.boredapi.com](www.boredapi.com) is hosted on Heroku. 


### Installation

To install and host this project on your own machine, do the following:
1. Install Node.js and MongoDB.
2. Clone the project from https://github.com/drewthoennes/Bored-API.
3. Start MongoDB instance, change directory into the clone project and run

```
npm install
npm start
```
4. The application is available on https://hostname/8080


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


## Appendix

### Future feature suggestions


### Known issues

### Error code

### Suggestions for changes









