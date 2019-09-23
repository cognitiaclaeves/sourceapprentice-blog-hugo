+++
author = "cognitiaclaeves"
comments = true
date = "2019-09-11T14:30:00+00:00"
discussionId = ""
draft = true
lastmod = ""
summary = ""
tags = ["python", "web-server", "wsgi", "job-search"]
tags_old = []
thread = ""
title = "Workstuff and Birds of Prey"

+++
My recent job-search adventures have exposed me to a number of glimpses into how problems are being solved in the field. Not too long ago, I was asked to set up a CI/CD pipeline for a Spring application which exposed me to technology that I'd never played with. Most recently, I was invited to peruse a code-base for a feature that has yet to be released. In this case, I've got a glimpse of an application that has been implemented in a framework that I'd not been exposed to yet -- falcon. Falcon is so light-weight that its implementation looks a lot more like what an app might look like if it were built only with werkzeug, a python WSGI utility library.

## [werkzeug](https://werkzeug.palletsprojects.com "Python werkzeug")

To demonstrate its routing, the werkzeug site [offers the following example](https://werkzeug.palletsprojects.com/en/0.15.x/tutorial/#step-4-the-routing "werkzeug routing example"):

    def dispatch_request(self, request):
        adapter = self.url_map.bind_to_environ(request.environ)
        try:
            endpoint, values = adapter.match()
            return getattr(self, 'on_' + endpoint)(request, **values)
        except HTTPException, e:
            return e

Note: If, for some reason the link above doesn't work, the source code should be available in my [forked copy](https://github.com/cognitiaclaeves/werkzeug/blob/blog-example-201909/examples/shortly/shortly.py#L114 "Werkzeug shortly.py example"). ... I forked it because if the seemingly arbitrary implementation of the example ever changes, this blog post will lose its whole meaning.

In the example above, `dispatch&lowbar;request()` is called from `wsgi&lowbar;app()`, which appears to be called by implementing `&lowbar;&lowbar;call&lowbar;&lowbar;().` The execution of `dispatch&lowbar;request()` results in the execution of functions such as `on&lowbar;new&lowbar;url()`, where `new&lowbar;url` matches the endpoint of the url passed into the application.

As mentioned in the example, it's pretty much turtles all the way down. But what's interesting about this example, is that it almost seems that falcon's framework appears to build on this example, even though I think the implementation of the example itself might be pretty arbitrary. Maybe it's not as arbitrary as it seems to me.

## [falcon](https://falcon.readthedocs.io/en/stable/ "Python falcon")

Falcon appears to shift the implementation of the functions -- just a little bit -- in a way that seems to be in the same spirit of werkzeug. [Falcon also makes implementation decisions around the concept of REST applications](https://falcon.readthedocs.io/en/stable/user/tutorial.html#creating-resources "Falcon's framework design") -- whereas the endpoint for werkzeug was pretty arbitrary, falcon organizes around resources, and expects the endpoint to match a class, and within that class, it dispatches to functions such as `on&lowbar;get()` and `on&lowbar;post()`, depending on the type of call it processes.