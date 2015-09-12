# Logging from ServiceStack

##### [Thomas Ardal](http://elmah.io/about/), December 20, 2013 in [Tutorials](/category/tutorials/)

> This post has been adapted as part of our official documentation. To read the most updated version, please check out [Logging to elmah.io from ServiceStack](http://docs.elmah.io/logging-to-elmah-io-from-servicestack/)

Logging errors to elmah.io from ServiceStack is almost as easy as installing in MVC and Web API. The folks over at ServiceStack provide you with a NuGet package named ServiceStack.Logging.Elmah. Like Web API you need to tell ServiceStack to use ELMAH as logging framework for errors, besides adding the standard ELMAH configuration in web.config. Start by installing both ServiceStack.Logging.Elmah and elmah.io into your ServiceStack web project:

```powershell
Install-Package ServiceStack.Logging.Elmah
Install-Package elmah.io
```

Once installed, add the following line to your AppHost:

```csharp
LogManager.LogFactory = new ElmahLogFactory(new NLogFactory());
```

The above example assumes that you are already using NLog as the existing framework for logging. Wrapping different logger factories in each other actually makes it possible to log errors through ELMAH and other types of messages like warnings and info messages through another logging framework. If you don’t need anything other than ELMAH logging, use the NullLogFactory instead of NLogFactory.

That’s it! By installing both the ServiceStack.Logging.Elmah and elmah.io packages, you should have sufficient configuration in your web.config to start logging like a pro.