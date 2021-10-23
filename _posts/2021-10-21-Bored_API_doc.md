---
layout: post
title: "Bored API Quick Start Guide"
date: 2021-10-21
---

---

This blog documents the public web API Bored API available on [https://www.boredapi.com](https://www.boredapi.com). 

Readers are expected to have knowledge on web APIs. If not, please refer to my earlier blog [A beginner's guide to APIs](https://taolicd.github.io/2019/08/08/Intro_API_blog.html). 

---


## What is the Bored API?

The [Bored API](https://www.boredapi.com) is a web API where you submit queries and the API returns suggested things to do. You can narrow down the scope of suggestions by specifying certain criteria such as activity type or number of participants. If you do not specify any criteria, you will get a random suggestion.  


## Authentication and authorization
You do not need an API key or any username/password to use this API. 

## Installation and deployment 


The Bored API was built using  [MEVN stack](https://www.educative.io/edpresso/what-is-mevn-stack) with frontend using Vue.js and Webpack and backend using Node.js and MongoDB. The application on [www.boredapi.com](www.boredapi.com) is hosted on Heroku. You can use this hosted API for querying activities without deploying your own. 


If you do want to install and deploy this project on your own host, follow the steps below:

1. Install Node.js and install MongoDB.
2. Clone the project from [https://github.com/drewthoennes/Bored-API](https://github.com/drewthoennes/Bored-API).
3. Start MongoDB instance, change directory to the clone project from step 2 and run
```
npm install
npm start
```
4. The Bored API starts on https://hostname:8080.


## Endpoints

This API supports HTTP method `GET` on one endpoint: `/api/activity`.  See [Bored Swagger UI](https://taolicd.github.io/swagger-for-bored-api/) for details. The [swagger.yaml](https://github.com/taolicd/swagger-for-bored-api/blob/master/swagger.yaml) file was created by Tao and the [Bored Swagger UI](https://taolicd.github.io/swagger-for-bored-api/) is hosted under Tao's personal GitHub Pages.

## Example response

Here is an example Json response you may get from the API:

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
where

key | value 
--- | --- 
activity | Description of the suggested activity
type | Type of the activity from one of the 9 categories: ["education", "recreational", "social", "diy", "charity", "cooking", "relaxation", "music", "busywork"]
participants |The number of people from 1 to many that this activity will involve 
price | A price indicator describing the cost of the activity from [0.0, 1.0] with 0 being free and 1 extremely expensive
link | The URL related to this activity. This information is optional.
key |A unique numeric ID for this activity from [1000000, 9999999]
accessibility | An indicator from [0.0, 1.0] describing how easy or challenging an activity is with 0 being very easy and 1 extremely challenging


## Use cases

The Bored API has been used in other applications including

* [I'm Bored Alexa skill](https://www.amazon.com/gp/product/B07GDL9MP4?ie=UTF8&ref-suffix=ss_rw)
* [Python wrapper](https://pypi.org/project/bored/)
* [Kotlin wrapper](https://gitlab.com/CMDR_Tvis/bored-api)
* [React app](https://github.com/CDAracena/Im-Bored)
* [Vue app](https://github.com/emilsgulbis/BoredApp)
* [iOS app](https://apps.apple.com/us/app/bored-find-what-to-do/id1475656469)
* [Are you bored](https://ajaykarwal.github.io/bored/)



## Miscellaneous items to discuss with the developer (if I had a chance) 

### 1. HTTP response status code

Currently, the API does not return HTTP response status code 404 for result not found. For example, when I run the curl command below
  ```
  curl https://www.boredapi.com/api/activity?price=1
  ```
  I get `"error": "No activity found with the specified parameters"` in the Json response. If I curl the header

  ```
  curl -I https://www.boredapi.com/api/activity?price=1
  ```

The returned header shows HTTP status 200. I think having a return status code 404 for not found probably is more conventional and appropriate in this case.  

### 2. Potential future feature suggestions
* Currently the only HTTP method available is `GET`. What if we allowed users to post new activity suggestions in a "segregated" manner? For example, the existing activity entries will be tagged with a new attribute `status=official` and future user submitted activities will be assigned `status=user-submitted`. Once in a while the API administrator may go through the entries and change the status from `user-submitted` to `official` for any interesting new suggestions. We will support HTTP method `POST` and maybe even `PUT` or `DELETE` for user-submitted items. To have some control over random user submissions or deletions, we probably need to implement API authentication. For the `GET` method, it will continue to be authentication free and the new `status` attribute will be added as a parameter users can query on. 
* Currently only Json response is available. We can provide other response types such as txt, yaml, or xml. 
* Allow querying for multiple activities in one attempt. 

### 3. The `accessibility` parameter 

   The term `accessibility` can be a bit misleading. At first I thought it meant whether the activity is friendly to people with disabilities.  I suggest a more straightforward term such as `difficulty`. 


---
_Special thanks to [Drew](https://github.com/drewthoennes) for developing and sharing this interesting web API publicly._

---




