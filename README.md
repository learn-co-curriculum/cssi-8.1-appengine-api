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


## Conclusion / So What?


## Hints and Hurdles

+
