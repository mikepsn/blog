---
```

Remember the segments I talked about? You can configure which domains to load different kind of resources from using a range of different `*-src` keys like this:

```xml
<add name="Content-Security-Policy" value="default-src 'self'; script-src 'self' https://cdnjs.cloudflare.com; style-src 'self' https://maxcdn.bootstrapcdn.com" />
```

This configuration let your web application load resources from its own domain plus scripts from `cdnjs.cloudflare.com` and stylesheets from `maxcdn.bootstrapcdn.com`. The combinations are endless, so check out the [documentation](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy) on Mozilla.org for details.

Chances are, you don't have a document where every dependency of your website is written down. Implementing the `Content-Security-Policy` header therefore takes time and digging. The best approach is to start limiting resources to `self` and testing the entire web application and see if it works or not. If running with developer tools open in Chrome or whatever browser may be your favorite, the Console will tell you when your web app tries to fetch or execute code not allowed in the header:

![Content-Security-Policy results in the console](images/content-security-policy-report.png)

Another approach to catching all needed configuration, is to start by using an alternative header named `Content-Security-Policy-Report-Only`:

<add name="Content-Security-Policy-Report-Only" value="default-src 'self'" />

By adding this header instead of `Content-Security-Policy`, the browser will keep telling when something isn't allowed, but allow it anyway. This way you can keep an eye on the console, when running your website in production. When all error messages in the console are gone, you switch back to the original header.

Constantly keeping an eye the console and trying to touch all pieces of code in your application can be hard. In the following post, I will show you how to use elmah.io to monitor the output of the `Content-Security-Policy` header.