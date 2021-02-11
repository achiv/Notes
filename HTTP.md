# Milestone #1 - Intro to HTTP
* HTTP - HyperText Transfer Protocol.
* When we enter a website URL, the browser creates a HTTP Request on our behalf and sends it to the server on which the website is hosted. The HTTP Response from the server is read by the browser and rendered for us beautifully as web pages instead of the raw HTML returned.
* Each of the images, CSS file, JavaScript file or any other resource the website uses requires an HTTP request each.

![HTTP Request Headers](https://raw.githubusercontent.com/achiv/Notes/main/images/HTTP_Request_Headers.png)

1. Request URL - URL of the resource fetched
2. Request Method - denotes the action to be done. "GET" is for fetching some resource
3. Status Code - denotes how the server responded to the request. "200 OK" means a successful request and as this is a “GET” request, server will have sent some data back i.e, website’s HTML content

### Q. How would the server know the Chrome version from which the request was made?
* Browsers sends a User-Agent request header along with HTTP requests to denote the software it’s using.
```
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/84.0.4147.105 Safari/537.36
```
### Q. Open a browser tab in Incognito. Visit https://crio.do/ after opening the Networks tab in DevTools. Observe the size of data transferred. Open a new tab and do the same. Is there a difference in the size of data transferred now?
* You’ll be able to see in the bottom of the pane the size of data transferred to load the website. This as shown here is 2.7MB the first time.
* When reloaded, the amount of data transferred got reduced to 806KB.
* This is due to using the if-modified-since in the HTTP request header and the last-modified response header the server sends. These values are used by the server to determine if to send any resource again.
* To make websites load faster, websites make use of caching by which resources like images are saved by the browser when it visits a website. HTTP provides headers for the server to specify how this has to happen.

![CC Ans1](https://raw.githubusercontent.com/achiv/Notes/main/images/CuriousCatAns.png)

### Q. Is there any order in which the resources are loaded?
* Though it might seem CSS & JavaScript files are preferred over images, HTTP doesn’t favor any particular type of files to be loaded first. Further HTTP requests to fetch required resources for a page are made asynchronously meaning that each request is made independently without waiting for other requests to complete. As images are mostly of larger size than other resources, these requests get completed the last.Order in which resources are requested can also depend on their relative ordering in the HTML file.

### Q. HTTP is a ‘stateless protocol’, meaning two corresponding requests do not share data - your prior request is not ‘remembered’ in any way by the following one - this obviously has some flip sides - you might need to keep resending data that you want to persist through requests - why is it still designed this way?
* The reason for statelessness is load-balancing : modern day web isn’t just about one server or one client always - your one request could go to a server in North Virginia, the next to someplace in California - to manage traffic. And this means that you can’t really have one server holding on to data that it might never be using

<hr>

# Milestone #2 - HTTP Request Methods
We can use HTTP to:
* Upload data to the server eg: Add profile picture to facebook
* Update some data present in the server eg: Change your facebook display name
* Delete some data present in the server eg: Remove contact information from facebook

## GET
* GET requests are used to "get" resources from a server. By definition, GET requests **should **only fetch data from the server and shouldn’t change the data stored on the server.
* We can only specify a single resource in the HTTP request-line at a time meaning that we need a separate HTTP request for fetching any related files (image, css, javascript) the HTML needs.

## POST
* POST requests are used to send some data to the server. Some use cases are to submit data from a web form or to upload a file to the server.

## PUT
* PUT requests are used to update data on the server side. This could be for actions like changing your Facebook relationship status, updating a student’s marks on the college server after improvement exams etc.

#### NOTE: Preserve log is a checkbox that lets you persist logs between page refreshes. This is useful when debugging website issues that require you to refresh the page, since all console output is otherwise cleared

![HTTP Request Methods](https://raw.githubusercontent.com/achiv/Notes/main/images/HTTP_Request_Methods.png)

### Q. Is it possible to send form data using a GET request? Why or why not?
* Yes, it’s possible though not recommended. Usually, form data contains fields that are sensitive like passwords and using GET requests for submitting these means your password will be out in the open along with the request URL.

### Q. Are there any limitations in using a GET request to send data to the server?
* Data in a GET request is sent as part of the URL and this has a limit of 2048 characters.

### Q. If you were to add 5 images to your HTML file using <img>, how many extra HTTP GET calls will it result in?
* 5 extra HTTP GET calls, each retrieving an image.

### Q. Which of the following are true regarding HTTP POST and HTTP PUT requests?
* POST request is usually used to create a new resource whereas PUT is usually used to update an existing resource. Nevertheless, both can be used to create a new resource based on the requirement.
* Submitting a form data is usually a POST request whereas updating your profile picture could be a PUT request
* POST isn’t idempotent as sending 10 POST requests can create 10 new identical resources.
* PUT is idempotent as sending 10 PUT requests will still be updating the existing resource only. 

<hr>

# Milestone #3 - HTTP Status Codes
* HTTP Status codes are part of the HTTP Response.
* Status codes are 3 digit numbers (201, 304 etc) and are categorised to 5 different families based on their starting digit.
* Along with the status code, a Reason-Phrase is also present (OK, Moved Permanently etc).

## Status codes - 1xx
* Informational responses

## Status codes - 2xx
* Successful responses
* The 2xx family of status codes or status codes 200-299 signifies the HTTP request was successfully received & understood by the server.

## Status codes - 3xx
* Redirects
* 3xx family of status codes denotes that further action must be taken to complete the HTTP request made.
* Try navigating to http://www.flipkart.com instead of https://www.flipkart.com (http instead of https)
* The response status code: 301 Moved Permanently. This is Flipkart asking the browser to redirect the request from the unsecure URL (http://) to the secure URL (https://) instead. The browser will oblige and send the request accordingly.

## Status codes - 4xx
* Client errors
* Getting a 4xx status code tells us that there was an error in the HTTP request sent by the client (browser).

## Status codes - 5xx
* Server errors
* The 5xx class of codes are responses to requests that servers fail to fulfill.

### Q. When you try to access a resource that requires logging in, like LinkedIn feed, https://www.linkedin.com/feed, you get redirected to the login screen. That should be a 301, right?
* That was a 302 instead of 301. While 301 denotes a permanent redirect, 302 says the requested resource is temporarily unavailable.
* Here, 302 is used as the requested resource was found, there just is another page to go through (Login page) before it can be accessed.

### Q. One day or another, you’d have come across the below pop-up when trying to reload a web page containing a form. Why does this happen? Is there any way to avoid this happening?
```
Confirm Form Resubmission
The page that you're looking for used information that you entered. 
Returning to that page might cause any action that you took to be repeated.
Do you want to continue?
```
#### The Post/Redirect/Get (PRG) Pattern
* This happens when the user tries to refresh or use the back button to navigate back to a HTTP POST.
* A typical case where you might see this is when checking out from a web store. Maybe you have one page that takes your shipping address, and a second page that takes your billing information. The first page submits your data with an HTTP POST, and then returns a 200 response with the payment details form HTML. If the user hits the back button in their browser, or tries to refresh the second page, they will see one of the above dialogs.
* To avoid this usability issue, you want to try to keep POST events out of the browser history. Conveniently, there there is a mechanism for this that all the browsers respect. If a HTTP POST returns a HTTP 302 redirect, only the location of the redirect will be stored in the browser history. Hitting the back button will skip over the POST, and the user can bounce freely between the first and second forms.
#### Bad Code
```python
def view_record(request, record_id):
    record = get_object_or_404(Record, pk=record_id)
    if request.method == "POST":
        record.name = request.POST.get("name")
        record.save()
    return render_to_response("page.html", locals())
```
#### Good Code
```python
def view_record(request, record_id):
    record = get_object_or_404(Record, pk=record_id)
    if request.method == "POST":
        record.name = request.POST.get("name")
        record.save()
        return HttpResponseRedirect(reverse("view_record", args=[record_id]))
    return render_to_response("page.html", locals())
```

### Q. Find out example situations that result in a 4xx or 5xx response code.
* We can get a 4xx status code if 
  * Syntax of the HTTP request is wrong
  * Username or password provided is invalid
* We can get a 5xx status code if
  * Server is down :(
  * Server is overloaded with requests 

### Q. What is the status code you get when you type http://crio.do?
* 301 - Moved Permanently

<hr>

# Milestone #4 - Setup
* Execute curl -V in the terminal to check if the cURL utility is installed.

<hr>

# Milestone #5 - cURL and Postman
## The cURL Utility
* cURL is like a web-browser, but for the command line.You can make HTTP requests using cURL just like in a web-browser. The Response can be seen on the command line or redirected to a file.
```
curl -X GET https://www.flipkart.com -o ~/flipkart.html
```
* The output of the curl command goes to a file called flipkart.html. You can type ```cat ~/flipkart.html``` to see the contents of flipkart.html file.
* In the above ```curl``` request, ```-X``` allows you to specify the HTTP method to be used.
* You don’t have to use the ```-X GET``` switch => it is the default behaviour. Try the following command: ```curl https://www.flipkart.com```
* We can also print the HTTP Response Headers using this: ```curl -i -X GET http://www.flipkart.com -o flipkart.html```
* For verbose logs, ```curl -v -X GET http://www.flipkart.com -o flipkart.html```
* Redirect uRL automatically using the ```-L``` switch => ```curl -v -L -X GET http://www.flipkart.com -o flipkart.html # still using http and not https```

<hr>

# Milestone #6 - Construct a simple HTTP request from scratch
* The telnet client helps us connect to other computers on the internet. The format is telnet hostname port
#### Opening a TCP connection to server via telnet
```
crio-user@crio-demo:$ telnet data.pr4e..org 80
Trying to 192.241.136.170...
Connected to data.pr4e.org.
Escape character is '^]'.

```

![HTTP RR](https://raw.githubusercontent.com/achiv/Notes/main/images/contruct_HTTP.png)

* From the above figure, different parts of the HTTP communication are:
  * Request Line (HTTP Request)
  * Status Line & Response Header (HTTP Response)
  * Response Body (HTTP Response)

<hr>

# Milestone #7 - Takeaways
## Summary
* HTTP is an application layer protocol that allows transfer of data between machines. Most common use of HTTP is in loading web pages where HTML documents are fetched along with the other resources like images, CSS & JavaScript that it uses
* HTTP Request Method - used by the system requesting the resource to specify the type of request
  * GET - can be used to fetch web pages
  * POST - can be used to submit login data
  * PUT - can be used to update data
  * Other HTTP methods are HEAD, DELETE, OPTIONS, CONNECT, TRACE & PATCH
* HTTP Response Status Code - seen in the response message. Used by the system receiving the request, to specify the result of the request.
  * 1xx - Informational responses
  * 2xx - Successful responses eg: 200 OK - Request successfully completed
  * 3xx - Redirects eg: 301 Moved Permanently - Requested resource was moved permanently to a different location
  * 4xx - Client errors eg: 404 Not Found - Requested resources wasn’t found
  * 5xx - Server errors

## Interview Corner
* What is HTTP? Why was it introduced?
* What happens when you type google.com in a browser?
* What are the main HTTP verbs/methods?
* What are the different HTTP response codes?
* What is the difference between HTTP and HTTPS?
* What is cURL?
* What is Postman used for?

<hr>






































