# Milestone #1 - Getting Started with REST APIs
* REST stands for REpresentational State Transfer.
* API stands for Application Programming Interface
* REST APIs are those APIs which follow the guidelines set by the REST architecture. They follow a client-server model where one software program sends a request and the other responds with some data. REST APIs commonly use the HTTP protocol to send requests & receive responses.
* How an API request differs from a usual HTTP request for a webpage, is in terms of the data returned. HTTP requests for webpages return HTML, CSS & JavaScript files which are rendered by the browser and displayed to the user. But, in the case of APIs, the request can be for any data (not just webpage) and the response is read by the requesting program which interprets the data.
* The data format in REST is usually JSON. XML is another popular format for data transfer between applications.

### Q. Are the API endpoints case sensitive i.e, if requests to /location & /Location must return the same response? Try it out for https://www.metaweather.com/api/location/search/?query=san
* The case-sensitivity of endpoints isn’t a constraint that REST imposes but comes up because we’re using HTTP for communication. For HTTP, the scheme & hostname are case-insensitive and the rest of the part is case-sensitive (for https://www.metaweather.com/api/location/search/?query=san scheme is https and hostname is www.metaweather.com)

### Q. Why is it that you are able to make a REST API call via the browser?
* REST API calls are made on top of HTTP requests. Browsers as we know can make HTTP requests (they can visit web pages, right?) and hence can also make REST API calls that are made via HTTP, as long as they can interpret the data that is received in the response.

<hr>

# Milestone #2 - Anatomy of REST API
* Let’s look at the different components of the REST API request.
  1. Request URL: https://www.metaweather.com/api/location/search/?query=san
  2. Request Method: GET which denotes the type of HTTP request made. GET means data needs to be fetched.
  3. Request Headers: eg: accept, accept-encoding - used to send additional info like the type of encoding that the requesting application (browser) supports
  4. Request Body: is empty for the current request but can be used for sending additional information like a file’s content when uploading it to the server.

![REST Anatomy](https://raw.githubusercontent.com/achiv/Notes/main/images/REST-anatomy.png)

* The Request URL is made up of the
  1. Scheme: https - denotes the request was made using the HTTPS protocol ie, secure version of the HTTP protocol
  2. Root-endpoint: www.metaweather.com - defines the API provider
  3. Path: /api/location/search/ - there will be one api path for each type of resource. Here, we are asking for the resource named location.
  4. Query parameter: ?query=san - the part of the URL that comes after a ? character is the query parameter. It specifies the search criteria for the resource. Here, the locations returned get filtered by the value of the query parameter, query we provide.

* For every API request, the corresponding API response also contains HTTP headers that the server sends back along with the data requested.

![API Response Headers](https://raw.githubusercontent.com/achiv/Notes/main/images/REST_respone_headers.png)

### Q. What are the HTTP methods this API endpoint supports?
* GET, HEAD, OPTIONS

### Q. What is the data format sent by the server?
* application/json

### Q. Check the response encoding used. Was it included among the accept-encoding request header sent to the server?
* gzip, Yes.

### Q. Let’s say we need to use another parameter, country along with the query parameter to filter the locations for a particular country. How would we redesign the request URL, https://www.metaweather.com/api/location/search/?query=san for this purpose? (Note: the Metaweather API doesn’t support country parameter)
* Search parameters come after the ? character. Multiple search parameters can be used by separating them with the & character.
* For an API that needs to take two search parameters - query(city) and location (country), the request URL should be like this https://www.metaweather.com/api/location/search/?query=san&location=India

### Q. The API server is https://cat-fact.herokuapp.com and the API endpoint is /facts. How do you create the URL to make the API call?
* https://cat-fact.herokuapp.com/facts

<hr>

# Milestone #3 - REST API calls using programs

### Q. Try doing a POST request for  https://www.metaweather.com/api/location/search/?query=san. What is the status code of the response received?
* HTTP 405 response code is returned as the endpoint only allows GET request. 
```
Status: 405 (Method Not Allowed)
{
  "detail": "Method \"POST"\ not allowed."
}
```
* We can use the curl command to send a POST request. You can try this online curl utility.
```
curl -X POST https://www.metaweather.com/api/location/search/?query=san
```


### Q. Which of the following can be used to call a REST API?
* Browser
* cURL
* Python program
* Android app

<hr>

# Milestone #4 - Out in the Real World!
* Share a post on LinkedIn - "Got introduced to REST API!" using cURL.
* But, how did LinkedIn know whose account to post the message to?
* If you observe carefully, you will see cookies from the browser get sent as a part of the request. This is what LinkedIn uses to identify your account. This cookie gets refreshed periodically, so it may not remain valid forever. A new one would be generated after a while.

<hr>

# Milestone #5 - Takeaways
## Summary
* APIs makes it easier for
  * Applications to expose their services
  * Other applications to avail those services.
  * Integration is easier, only the API definitions need to be exposed.
* The internet is full of such APIs and the knowledge of APIs will help you utilize these services as well as to develop new ones of your own

## Interview Corner
* What’s REST and how it differs from GraphQL?
* What’s an API, how do you ‘hit’ an API? How do you query APIs?
* What are three things you’ll keep in mind when creating a REST API?







