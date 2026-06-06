# 2026-06-06-17-47-22-UTC-plus-2-HTTP-cookies.md



## Sources

- https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/Cookies

- https://en.wikipedia.org/wiki/HTTP_cookie



## Introduction

[Recall that]
by default the HTTP protocol is [stateless](
    https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/Overview#http_is_stateless_but_not_sessionless
).

---

A «cookie» (also known as a «web cookie» or «browser cookie») is
a small piece of data a server sends to a user's web browser.
The browser may
- store cookies,
- create new cookies,
- modify existing ones, and
- send them back to the same server with later requests.

Cookies enable web applications to store limited amounts of data and remember state information

---

An «HTTP cookie» (also called «web cookie», «Internet cookie», «browser cookie», or «simply cookie»)
is a small block of data
created by a web server while a user is browsing a website
and
placed on the user's computer or other device by the user's web browser.
Cookies are placed on the device used to access a website,
and more than one cookie may be placed on a user's device during a session.



## Uses



Session management



1. logging into websites. When the user visits a website's login page, the web server typically sends the client a cookie containing a unique session identifier. When the user successfully logs in, the server remembers that that particular session identifier has been authenticated and grants the user access to its services.

  - At a later time, the user moves to a different page on the same site. The browser sends the cookie containing the session ID along with the corresponding request

  - The server checks the session ID and, if it is still valid, sends the user a personalized version of the new page. If it is not valid, the session ID is deleted and the user is shown a generic version of the page (or perhaps shown an "access denied" message and asked to sign in again).



2. Cookies were originally introduced to provide a way for users to record items they want to purchase as they navigate throughout a website (a virtual «shopping cart» or «shopping basket»). Today, however, the contents of a user's shopping cart are usually stored in a database on the server, rather than in a cookie on the client. To keep track of which user is assigned to which shopping cart, the server sends a cookie to the client that contains a [unique session identifier](
    https://en.wikipedia.org/wiki/Unique_identifier
) (typically, a long string of random letters and numbers). Because cookies are sent to the server with every request the client makes, that session identifier will be sent back to the server every time the user visits a new page on the website, which lets the server know which shopping cart to display to the user.



3. game scores



4. any other user session-related details that the server needs to remember



> Because session cookies only contain a unique session identifier, this makes the amount of personal information that a website can save about each user virtually limitless—the website is not limited to restrictions concerning how large a cookie can be. Session cookies also help to improve page load times, since the amount of information in a session cookie is small and requires little bandwidth.



---



Personalization



Cookies can be used to remember «user preferences» such as display language and UI theme.



---




Tracking



Recording and analyzing user behavior.



to track users' web browsing habits. This can also be done to some extent by using the [IP address](
    https://en.wikipedia.org/wiki/IP_address
) of the computer requesting the page or the [referer](
    https://en.wikipedia.org/wiki/HTTP_referer
) field of the [HTTP](
    https://en.wikipedia.org/wiki/HTTP
) request header, but cookies allow for greater precision. This can be demonstrated as follows:

- If the user requests a page of the site, but the request contains no cookie, the server presumes that this is the first page visited by the user. So the server creates a unique identifier (typically a string of random letters and numbers) and sends it as a cookie back to the browser together with the requested page.

- From this point on, the cookie will automatically be sent by the browser to the server every time a new page from the site is requested. The server not only sends the page as usual but also stores the URL of the requested page, the date/time of the request, and the cookie in a log file.

By analyzing this log file, it is then possible to discover which pages the user has visited, in what sequence, and for how long.
