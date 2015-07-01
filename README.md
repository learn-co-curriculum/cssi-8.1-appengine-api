---
tags: api, appengine, python, json
level: 3
languages: python, json
---

# API's

## Objectives

+ Understand how API's connect services on the web
+ Understand how Client Library's wrap API functionality
+ Understand how AppEngine provides it’s own API libraries
+ Use the AppEngine Users API module
+ Connect to any public facing API
+ Access the returned data from an API

## Motivation / Why Should You Care?

API’s (Application Programming Interfaces) are a major part of the internet and allow amazing things to happen easily. There are TONS of cool ways to connect other applications to extend our app's functionality. Want to include GIFs based on user searches? Show Tweets related to your site? We can do this and much, much more using APIs!

## Lesson Plan

### What is an API?

+ API stands for "Application Programming Interface".
+ In a nutshell, an API is a set of instructions that allows developers to change and control existing web applications. It's a way for the developers of existing applications to allow other people to get their data in a controlled way.

### Client Wrapper Libraries for API's

Sometimes developers will provide you with a class/module/library that makes connecting to an API much easier.  They will make sure that the correct language for that API is used and all you have to do is use the (hopefully) simple methods that they provide.  

### App Engine Users API

The AppEngine Users module actually connects to Google’s User authentication service.  However for a developer the setup is very easy and allows you to have Authenticated (signed in and verified) users that you can trust; they’re backed by Google.

Using this API Library is as simple as importing the `users` module from `google.appengine.api` and using the built in methods that are provided. Here's a very simple example of how that works.

```python
from google.appengine.api import users
import webapp2
class MyHandler(webapp2.RequestHandler):
    def get(self):
        user = users.get_current_user()
        if user:
            greeting = ('Welcome, %s! (<a href="%s">sign out</a>)' %
                        (user.nickname(), users.create_logout_url('/')))
        else:
            greeting = ('<a href="%s">Sign in or register</a>.' %
                        users.create_login_url('/'))

        self.response.out.write('<html><body>%s</body></html>' % greeting)
```

### Using an API

Every API is a little bit different, but in general we can follow a process for connecting to them.

1. Read the documentation.
2. Setup an "API call" - going to get the data
3. Deciding what to do when you get the data back

Sometimes, APIs are well documented and we can follow the instructions easily. Other times, they're not so well documented and we'll have to play around a bit more. For the most part, the APIs we use will give us back JSON objects that we can parse and get data from which can look like this.

```js
"students":[
	{"firstName":"John", "lastName":"Doe"},
	{"firstName":"Anna", "lastName":"Smith"},
	{"firstName":"Peter","lastName":"Jones"}
]
```

In the example above, the object "students" is an array containing three objects. Each object is a record of a CSSI student (with a first name and a last name).

### Calling the giphy API with `urllib`

This code will display the *raw* data the the API returns. Interesting, but not terribly useful.

```python
import urllib

class MainHandler(webapp2.RequestHandler):
    def get(self):
        data = urllib.urlopen(
     "http://api.giphy.com/v1/gifs/search?q=+ryan+goslin&api_key=dc6zaTOxFJmzC&limit=10").read()
        self.response.out.write(data)
```

### Loading JSON data

To make the JSON data more useful we need to load and parse it using `json.loads()`

```python
parsed_data = json.loads(urllib.urlopen(      "http://api.giphy.com/v1/gifs/search?q=+ryan+goslin&api_key=dc6zaTOxFJmzC&limit=10").read())
self.response.out.write(parsed_data)
```

Then we will need to navigate to the data that we want show which in this case might be `parsed_data['data'][0]['images']['original']['url'])`.

## Conclusion / So What?

API's are the way that web applications talk to each other. They will allow you use and incorporate advanced functionality and leverage existing services in your applications.

## Hints and Hurdles

+ API's are a great way to add additional functionality
+ Make sure you read the documentation for API's, they all work a little differently
+ There are great tools out there to help you work with API's such as [hurl](https://www.hurl.it/), [postman](https://www.getpostman.com/), and [apiary](https://apiary.io/)
