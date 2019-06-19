---
template: post
title: Fiddler - A quick starter
slug: /posts/fiddler-quick-starter
draft: false
date: 2019-06-03T03:58:31.168Z
description: >-
  Fiddler allows you to record, inspect, modify and generate HTTP traffic
  between clients and servers. Read on to learn basics of fiddler.
category: web-dev
tags:
  - web-dev
  - http
  - fiddler
---
[Fiddler][1] is a great tool if you are a web application developer or a performance or automation tester. It allows you to record, inspect, modify and generate HTTP traffic between clients (eg. a web browser or mobile app) and servers. It is installed on your desktop and it can help you setup a proxy server which can listen to the communication between apps running on you system and server.

## Setup
Download and install fiddler by visiting [this link][2]. It is currently in beta for OSX & linux at the time of writing this blog. Works great for Windows though. The example shown below are mostly from Windows perspective but it will work for other platforms the same way.

## Getting started
Assuming you have installed Fiddler, start it up by launching the app from start menu. 

![here is how it looks][3]

Go to the Tools > Options > HTTPS 

![Fiddler options https][4]

Tick the checkbox for Decrypt HTTPs traffic which will require you to trust fiddler generated certificate as a root certificate. Also, click the actions and trust 

![fiddler > actions > trust root certificate][5] 

Another interesting tab in options is connection. It clearly explains which port is used by fiddler to setup the proxy server. Using that you can manually setup the client or if you are following the instructions above, you are ready to start capturing.

![fiddler > options > connections][6] 

Now, if you open your web browser, say chrome and go to `https://www.google.com.au/` you should see something like below in fiddler. If for some reason, it doesn't appear at this point, follow [this guide.][7]

![fiddler capturing][8]

1. Session List - you need to click/select a session to view its details
2. Inspector view - has details about the session
3. Request view - related to client request
4. Response view - related to server response

Let's focus on request and response object views. What I have selected in the figure below is __Raw tab__ which basically contains all the information about them. All the other tabs are just different way of presenting the same information. Like __Headers tab__ is more focussed on request or response headers and displays them in tree view. __TextView__ and __SyntaxView__ displays the request/response body.

![request and response](//images.ctfassets.net/yvcmf0lc3wc3/7LU2nIZMpLfXkYeAAKrFId/04ba918d20bd17e6d07a0c2a7fdd1a64/image.png)

``` http
GET https://www.google.com.au/ HTTP/1.1
Host: www.google.com.au
Connection: keep-alive
Pragma: no-cache
Cache-Control: no-cache
Upgrade-Insecure-Requests: 1
User-Agent: Chrome/75.0.3770.80 Mobile Safari/537.36
DNT: 1
Accept: */*
Accept-Encoding: gzip, deflate, br
Accept-Language: en,en-GB;q=0.9,en-US;q=0.8
Cookie: SID=ZweS0XMsl21q-
```

Its clear from above that http messages are human readable. The first line in above code snippet has the method `GET` and `path` to the resource that is being requested using protocol `HTTP/1.1`. Rest of the request is `headers` and in some case it can contain the `body` of the request.

![http request](//images.ctfassets.net/yvcmf0lc3wc3/47GAmW6tTl0CtJpmT8jtaq/91d341c3490c4c65a3af4238546d68b6/image.png)

Response object usually contains `protocol`, `status code`, `status message`, `headers` and optionally a `body`.

``` http
HTTP/1.1 200 OK
Content-Type: text/html; charset=UTF-8
Strict-Transport-Security: max-age=31536000
Date: Tue, 18 May 2019 04:05:35 GMT
Server: gws
Content-Length: 135802
X-XSS-Protection: 0
X-Frame-Options: SAMEORIGIN
Expires: Tue, 18 May 2019 04:05:35 GMT
Cache-Control: private
Set-Cookie: 1P_JAR=2019-05-18-04; expires=Thu, path=/; domain=.google.com.au
Alt-Svc: quic=":443"; ma=2592000; v="46,44,43,39"

<!doctype html>
<html lang="en-AU">
<head>
<title>Google!</title>
</head>
<body>

...

</body>
</html>
```

![http response](//images.ctfassets.net/yvcmf0lc3wc3/tSOPYByyE9apR2lQduBFi/fcb4a8f2c9416def90a89e0f0a832858/image.png)

> HTTP is an extensible protocol that is easy to use. The client-server structure, combined with the ability to simply add headers, allows HTTP to advance along with the extended capabilities of the Web.
<cite>- [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview)<cite>

With a tool like fiddler, you can visualize and do a lot more with these captured traffic. It allows you to save these captured data in an archive file with `.saz` extention and view or edit them in future.


[1]: https://www.telerik.com/fiddler "Fiddler"
[2]: https://www.telerik.com/download/fiddler "Download Fiddler"
[3]: //images.ctfassets.net/yvcmf0lc3wc3/52GCxGjqtyN0q7f0RLlTjX/0680e32b90af08fb72c75239d2a18ae2/image.png
[4]: //images.ctfassets.net/yvcmf0lc3wc3/2is6SOxAts4p0DjRLw7obN/8e6591d6edae202982620bdc6ecf086a/image.png
[5]: //images.ctfassets.net/yvcmf0lc3wc3/kJLBhzAtqjv4cgqqaZfpb/f63169b779e0b1b7bc99787c1510eb4b/image.png
[6]: //images.ctfassets.net/yvcmf0lc3wc3/78daKte0SepO53GPgZ63hT/6dcf4cb00b553b425ffe80cedfdb5857/image.png
[7]: https://docs.telerik.com/fiddler/Observe-Traffic/Tasks/CaptureWebTraffic
[8]: //images.ctfassets.net/yvcmf0lc3wc3/6gBoIzjS3g0GyJbf7lIPaf/f38568b43d14c17f40730d97e78d437d/image.png