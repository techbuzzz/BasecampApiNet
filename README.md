# BasecampApiNet

![Logo](https://github.com/kgiszewski/BasecampApiNet/blob/master/assets/bcxnet.png)

This is a WIP .NET API wrapper for the BCX API for Basecamp. It returns staticly typed models and all is needed is the accountId, username and password.

##Install##
Depends on `Newtonsoft.Json` so you will need that if you don't already have it.

Otherwise you just need the current DLL in the release section.

You can also install via NuGet: https://www.nuget.org/packages/BasecampApiNet/1.0.0

##Syntax Example##

###All Projects###
`var project = new BasecampApiFactory().GetApi("account-id", "user", "password").Projects.GetAll();`

###Single Project###
`var project = new BasecampApiFactory().GetApi("account-id", "user", "password").Projects.Get(12345);`

###Reuse the Interface###

```
//get the api
//store this locally or globally
var api = new BasecampApiFactory().GetApi("account-id", "user", "password"); 
```
If the `api` variable goes out of scope, you'll lose your cache. You can wrap it in a static variable or use a singleton to persist it.

Simply using it in a class with a static reference will persist the cache for the life of your application:
```
using BasecampApiNet.Core;

namespace MyNamespace
{
    public class MyBasecampApi
    {
        public static BasecampApiBase Api = new BasecampApiFactory().GetApi("12345", "foo", "bar");
    }
}

```
Then you can simply reference the static variable in your code:

```
MyBasecampApi.Api.Projects.GetAll();

```

##WIP##
This wrapper is work in progress. 

Caching is in place with `MemoryCache`. If wish you can wrap this project into a Singleton to ensure the cache lasts as long as the application. This may be incorporated at some point.

Mostly Done:
* Project GET
* People GET
* TODOs GET
* UnitTests

Priority of work:

* GET requests (Events first)
* Everything else

##Contribute##
Send us a pull-request and it'll likely get merged!

###Everything Else###

I'd like to get to these:
* POST/PUT/DELETE verbs

##Based on BCX##
This wrapper is based on the official BCX API located here: https://github.com/basecamp/bcx-api

##Grunt##
This repo uses Grunt only for the purposes of building the Nuget releases and copying the DLL to a test application while editing the code.

To install Grunt you'll need NodeJs installed on your dev machine then run: `npm install`

You can then run the following if you wish:

Copy to a `/bin` folder:  `grunt --target="c:/dev/somedestination"`

Build Nuget package that outputs to your local `pkg` directory: `grunt nuget`
