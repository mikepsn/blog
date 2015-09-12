#Logging from Log4net

##### [Thomas Ardal](http://elmah.io/about/), April 28, 2014 in [Tutorials](/category/tutorials/)

> This post has been adapted as part of our official documentation. To read the most updated version, please check out [Logging from Log4net](http://docs.elmah.io/logging-to-elmah-io-from-log4net/)

log4net is probably the oldest .NET logging frameworks on the block. Maintained by Apache and developed for more than a decade, makes log4net a good and well supported choice for some types of applications. log4net is based on the concept of appenders, which works pretty much like ELMAH’s error logs. Unlike ELMAH, log4net can have multiple appenders, which makes it possible to log errors to multiple sources. In addition log4net supports different log levels like Info and Warning. While ELMAH doesn’t have the concept of log levels, elmah.io supports all of the levels in log4net.

In this tutorial we’ll add log4net to an ASP.NET MVC project, but the process is almost identical with other project types. Create a new MVC project and install the elmah.io appender:

```powershell
Install-Package elmah.io.log4net
```

Add the following to your AssemblyInfo.cs file:

```csharp
[assembly: log4net.Config.XmlConfigurator(Watch = true)]
```

Add the following config section to your web.config file:

```xml
<section name="log4net" type="log4net.Config.Log4NetConfigurationSectionHandler, log4net" />
```

Finally, add the log4net configuration element to web.config:

```xml
<log4net>
  <appender name="ElmahIoAppender" type="elmah.io.log4net.ElmahIoAppender, elmah.io.log4net">
    <logId value="LOG_ID" />
  </appender>
  <root>
    <level value="INFORMATION" />
    <appender-ref ref="ElmahIoAppender" />
  </root>
</log4net>
```

That’s it! log4net is now configured and log messages to elmah.io. Remember to replace LOG_ID with your actual log Id. To start logging, write your usual log4net log statements:

```csharp
var log = log4net.LogManager.GetLogger(typeof(HomeController));
try
{
    log.Info("Trying something");
    throw new ApplicationException();
}
catch (ApplicationException ex)
{
    log.Error("Error happening", ex);
}
```