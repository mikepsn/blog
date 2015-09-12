# Logging from Nancy

##### [Thomas Ardal](http://elmah.io/about/), Januar 6, 2014 in [Tutorials](/category/tutorials/)

> This post has been adapted as part of our official documentation. To read the most updated version, please check out [Logging from Nancy](http://docs.elmah.io/logging-to-elmah-io-from-nancy/)

As with MVC and WebAPI, Nancy already provides ELMAH support out of the box. Start by installing the elmah.io NuGet package:

```powershell
Install-Package elmah.io
```

To integrate Nancy and ELMAH, Christian Westman already did a great job with his Nancy.Elmah project. Install it using NuGet:

```powershell
Install-Package Nancy.Elmah
```

It’s important that you install the elmah.io package before Nancy.Elmah, because both packages likes to add the ELMAH configuration to the web.config file. If you install it the other way around, you will need to add the elmah.io ErrorLog element manually.

In order for Nancy to know how to log errors to Elmah, you need to add an override of the DefaultNancyBootstrapper. Create a new class in the root named Bootstrapper:

```csharp
using Nancy;
using Nancy.Bootstrapper;
using Nancy.Elmah;
using Nancy.TinyIoc;
 
namespace Elmah.Io.NancyExample
{
    public class Bootstrapper : DefaultNancyBootstrapper
    {
        protected override void ApplicationStartup(TinyIoCContainer container, IPipelines pipelines)
        {
            base.ApplicationStartup(container, pipelines);
            Elmahlogging.Enable(pipelines, "elmah");
        }
    }
}
```

The important thing in the code sample is line 13, where we tell Nancy.Elmah to hook into the pipeline of Nancy in order for it to catch and log HTTP errors. The second parameter for the Enable-method, lets us define a URL for the ELMAH error page, which can be used as an alternative to elmah.io for quick viewing of errors.