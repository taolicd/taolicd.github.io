---
layout: post
title: "Quickstart Guide to the Bored API"
date: 2021-10-20
categories: REST APIs
---

## What is the Bored API?

The [Bored API](www.boredapi.com) is a web API for submitting queries to find things to do to kill boredom. 


## Authentication 
You do not need an API key to use this API. Just submit a query to the endpoint `/api/activity/` to retrieve a suggested activity. 


## Installation and deployment 

The Bored API was built using  [MEVN stack](https://www.educative.io/edpresso/what-is-mevn-stack) with frontend using Vue.js and Webpack and backend using Node.js and MongoDB. The application on [www.boredapi.com](www.boredapi.com) is hosted on Heroku. You can use this hosted API for querying activities. 

If you want to install and deploy this project on your own host machine, follow the steps below:

1. Install Node.js and MongoDB.
2. Clone the project from https://github.com/drewthoennes/Bored-API.
3. Start MongoDB instance, change directory to the clone project and run
```
npm install
npm start
```
4. The application is started on https://hostname/8080


## Endpoint definitions

See [Bored swagger UI](https://taolicd.github.io/swagger-for-bored-api/) for details. The [swagger.yaml](https://github.com/taolicd/swagger-for-bored-api/blob/master/swagger.yaml) file was created by me (Tao) and the SWagger UI is hosted under my personal GitHub Pages.

## Example response

Here is an example Json response:

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

The Bored API has been used in other applications including

* [I'm Bored Alexa skill](https://www.amazon.com/gp/product/B07GDL9MP4?ie=UTF8&ref-suffix=ss_rw)
* [Python wrapper](https://pypi.org/project/bored/)
* [Kotlin wrapper](https://gitlab.com/CMDR_Tvis/bored-api)
* [React app](https://github.com/CDAracena/Im-Bored)
* [Vue app](https://github.com/emilsgulbis/BoredApp)
* [iOS app](https://apps.apple.com/us/app/bored-find-what-to-do/id1475656469)


### Future feature suggestions

* Add API authentication. This will be useful if we decide to support POST, DELETE, UPDATE operations in the future.
* Currently the only verb supported is GET. I suggest that we also support other verbs such as PUT, POST, DELETE for autherized users. 
* Provide other response types such as txt or yaml. 
* Allow query multiple activities at the same time. 


### Known issues

Currently, the application does not return standard HTTP response status codes such as 200 and 404. When a query returns no value, it returns `"error": "No activity found with the specified parameters"`. Ideally we want status code 200 for successful return and status code 404 for error not found. 

### Other miscellaneous things to discuss

The `accessibility` parameter can be vague and misleading. At first I thought it meant functionality that helps disable or impaired people.  I suggest a more straightforward term such as `difficulty`. 








