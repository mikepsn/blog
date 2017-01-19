# ASP.NET Core Tutorial
- [Config transformations in ASP.NET Core](config-transformations-in-aspnetcore.md)
- [Configuration with Azure App Services and ASP.NET Core](configuration-with-azure-app-services-and-aspnetcore,md)

### Middleware

Much like OWIN and Node.js, Core uses the concept of middleware. Middleware are code components executed as part of the application pipeline. You will find middleware for a lot of different purposes like logging, exception handling, routing etc.

We wrote a blog post about middleware as well:

- [Error Logging Middleware in ASP.NET Core](error-logging-middleware-in-aspnetcore.md)

### Logging

Core comes with a new logging framework called Microsoft.Extensions.Logging. If you want to know more about logging, read through our blog post:

- [ASP.NET Core Logging Tutorial](aspnetcore-logging-tutorial.md)

### Routing

Routing in its basic form, works much like in previous versions of ASP.NET. When looking into the details, you quickly spot some new features and fixes, that makes routing in Core really awesome. We blogged about routing here:

- [ASP.NET Core Routing Tutorial](aspnetcore-routing-tutorial.md)

### Error Handling

Error handling in Core is something that we are particular interested in :-) Stay tuned for future blog posts about the subject and make sure to check out our [elmah.io middleware for ASP.NET Core](http://docs.elmah.io/logging-to-elmah-io-from-aspnet-core/).

### Dependency Injection

Dependency injection always were a bit of a hack in ASP.NET. Since Core has been designed from the ground up, dependency injection is provided out of the box. The DI framework in Core doesn't necessarily replace your favourite IoC container, since it plays well with popular packages like Autofac and Windsor.

### Kestrel

Kestrel is a new webserver bundled with Core. Kestrel is a lightweight web server, built on top of libuv (yes, the same as Node.js). Kestrel is used to serve requests in Core, but it isn't intended to be serving requests towards the public. For that purpose, integrations for other web servers and reverse proxies have been made available from Microsoft. A popular choice for now, is to wrap Kestrel behind IIS, but serving Core behind Apache or nginx, seems like obvious choices as well.