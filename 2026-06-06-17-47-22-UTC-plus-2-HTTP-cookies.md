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



## `Set-Cookie` headers

After receiving an HTTP request, a server can send one or more `Set-Cookie` headers with the response, each one of which will set a separate cookie.

The following HTTP response instructs the receiving browser to store a pair of cookies:

```shell
HTTP/2.0 200 OK
Content-Type: text/html
Set-Cookie: yummy_cookie=chocolate
Set-Cookie: tasty_cookie=strawberry

[page content]
```

---

When a new request is made, the «browser engine» usually sends previously stored cookies for the current domain back to the server within a `Cookie` HTTP header:

```shell
GET /sample_page.html HTTP/2.0
Host: www.example.org
Cookie: yummy_cookie=chocolate; tasty_cookie=strawberry
```

## Attributes within a `Set-Cookie` header 

Each `Set-Cookie` header within an HTTP response can be supplemented with additional attributes,
which change how the client's browser is allowed to work with the cookie in question.

- If a `Set-Cookie` header is supplemented with an `Expires=Thu, 31 Oct 2021 07:28:00 GMT;` attribute,
  the browser will delete the cookie after the date specified

- If a `Set-Cookie` header is supplemented with a `Max-Age=2592000` attribute,
  the browser will delete the cookie after the period specified

- Cookies without a `Max-Age` or `Expires` attribute – are deleted when the current session ends. The browser defines when the "current session" ends, and some browsers use session restoring when restarting. This can cause session cookies to last indefinitely.

---

To update a cookie via HTTP,
the server can send a `Set-Cookie` header with the existing cookie's name and a new value. For example:

```shell
Set-Cookie: id=new-value
```

«JavaScript code running in a webpage»:

- can create new cookies via JavaScript using
  the [`Document.cookie`](
    https://developer.mozilla.org/en-US/docs/Web/API/Document/cookie
  ) property,
  or the asynchronous [Cookie Store API](
    https://developer.mozilla.org/en-US/docs/Web/API/Cookie_Store_API
  )

- can access existing cookies and set new values for them

- for security purposes,
  can't change cookie values
  by sending an updated `Cookie` header directly when initiating a request

There are good reasons why you shouldn't allow JavaScript to modify cookies at all. See the next sectio for more details.

---

Security:

- If a `Set-Cookie` header is supplemented with an `HttpOnly` attribute,
  then:

  - the «browser engine» is still able to read and send such a cookie
    (as part of every qualifying request)

  - but «JavaScript code running in a webpage» is completely blocked from reading it
    via `Document.cookie` or any other [browser] API

  ---

  This precaution helps mitigate [cross-site scripting (XSS) attacks](
    https://developer.mozilla.org/en-US/docs/Web/Security/Attacks/XSS
  ).

  The browser's internal cookie-handling machinery is opaque to the page.

- If a `Set-Cookie` header is supplemented with an `Secure` attribute,
  then:
  
  - it is only sent to the server with an encrypted request over the HTTPS protocol.
  
  - It's never sent with unsecured HTTP (except on `localhost`)

  - Insecure sites (with http: in the URL) can't set cookies with the `Secure` attribute.

  ---

  [This precaution helps mitigate [man-in-the-middle attacks](
    https://developer.mozilla.org/en-US/docs/Glossary/MitM
  ).]

---

- If the `Set-Cookie` header does not specify a `Domain` attribute,
  the cookie is available on the server that sets it
  but *not on its subdomains*.

- If the `Set-Cookie` header specifies a `Domain` attribute,
  the cookie is available on the specified server and its subdomains.

  > Note that
  >
  > a server can only set the `Domain` attribute to its own domain or a parent domain,
  >
  > not to a subdomain or some other domain.

---

- The `Path` attribute indicates a URL path that must exist in the requested URL
  in order to send the `Cookie` header.

- The `%x2F` ("/") character is considered a directory separator,
  and subdirectories match as well.

  For example, if the HTTP response sets
  
  ```shell
  Set-Cookie: id=a3fWa; Expires=Thu, 21 Oct 2021 07:28:00 GMT; Secure; HttpOnly; Path=/docs
  ```

  then these request paths match:

  - `/docs`
  - `/docs/`
  - `/docs/Web/`
  - `/docks/Web/HTTP`

  but these request paths don't:

  - `/`
  - `/docsets`
  - `/fr/docs`

<br />

---

<br />

> [Registrable domain](
>   https://developer.mozilla.org/en-US/docs/Glossary/Registrable_domain
> )
>
> A «registrable domain» is a domain
> that can be (or has already been) registered
> by an individual or an organization
> through a «domain name registrar». 
>
> «Registrable domains» are created directly underneath an «effective top-level domain» (eTLD),
> such as `.org`, `.com`, or `.ac.uk`.
> (
> For this reason a «registrable domain» is sometimes called an "eTLD+1".
> )
>
> For example, all of the following are «registrable domains»:
>
> ```
> crookedtimber.org
> theguardian.com
> sussex.ac.uk
> ```
> 
> All domains under a «registrable domain» belong to the same organization. For example:
> 
> ```
>  film.theguardian.com
> music.theguardian.com
> ```
> 
> ```
>       news.sussex.ac.uk
>       blog.sussex.ac.uk
> admissions.sussex.ac.uk
> ```
> 
> (
>
> Note that not all eTLDs are top-level domains, because many registrars allow organizations to register domains at levels below the top level. In the example above, `.ac.uk` is a subdomain of the top-level `.uk` domain, so `sussex.ac.uk` and `aber.ac.uk` can be registered to different organizations.
> 
> Because this is a matter of the registrar's policies, it's impossible to tell algorithmically whether a given domain name suffix (like `.ac.uk`) is publicly registrable or not. The [Public Suffix List](
>     https://publicsuffix.org/
> ) is a list of all suffixes under which organizations can directly register names: that is, it is a list of eTLDs.
>
> )
>
> ---
>
> [Site](
>   https://developer.mozilla.org/en-US/docs/Glossary/Site
> )
>
> [At the risk of repeating the preceding sub-section, let us recall that]
>
> - A «registrable domain» consists of an entry in the [Public Suffix List](
>   https://publicsuffix.org/list/
> ) plus [a string] just before it.
>
> - This means that, for example,
>   ```
>   theguardian.co.uk
>   sussex.ac.uk
>   bookshop.org
>   ```
>   are all «registrable domains».
>
> A «site» is determined by the «registrable domain» portion of the domain name.
>
> According to this definition,
> ```
> support.mozilla.org
> developer.mozilla.org
> ```
> are part of the same «site»,
> because `mozilla.org` is a «registrable domain».
>
> ---
>
> «Cross-site requests» are requests where the [«site»](
>     https://developer.mozilla.org/en-US/docs/Glossary/Site
> ) (the «registrable domain») and/or the scheme (http or https) do not match the «site» the user is currently visiting. This includes:
> 
> - requests sent when links are clicked on other sites to navigate to your site, and
> 
> - any request sent by embedded third-party content.



The `SameSite` attribute:

- lets servers specify whether/when cookies are sent with cross-site requests

- helps to prevent leakage of information,
  preserving user [privacy](
    https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/Cookies#privacy_and_tracking
  ) and providing some protection against [cross-site request forgery](
  https://developer.mozilla.org/en-US/docs/Glossary/CSRF
  ) attacks

- takes 3 possible values:

  - `Srtict`

    causes the browser to only send the cookie [when the browser issues] requests [to] the cookie's origin «site»

    should be used when you have cookies relating to functionality that will always be behind an initial navigation, such as
    - authentication
    - storing shopping cart information

    example:
    ```
    Set-Cookie: cart=110045_77895_53420; SameSite=Strict
    ```

  - `Lax` (default, if no `SameSite` attribute is set)

    similar, except the browser also sends the cookie when the user *navigates* to the cookie's origin «site» (even if the user is coming from a different «site»)

    useful for affecting the display of a «site», e.g.
    
    - «site» A might have partner product information along with an affiliate link (to «site» B)
    
    - When that link is followed to «site» B (= the partner website),
      «site B» might set a cookie indicating that an affiliate link was followed
    
    - on what kinds of requests to «site» B will the browser send the cookie?

      (a) in the case of a navigation that the user consciously initiated

        - If the user is already on «site» B and clicks around,
          the cookie is sent. Same site, no question.

        - If the user performs «top-level navigation» to «site» B
          (such as clicking a link from anywhere, including «site» A again; typing a URL; etc.),
          the cookie is sent.

      (b) in the case of background/embedded «cross-site requests»

        - If «site» A embeds an `<img>` or `<iframge>` pointing to «site» B,
          the cookie is NOT sent.
        
        - If «site» A has an `<img src="https://site-B.com/pixel.gif">`
          loading silently in the background,
          the cookie is NOT sent.

        - If «site» A is trying to silently ping «site» B in the background
          the cookie is NOT sent.
        
        - In the case of invisible background requests that would let «site» B know
          "this user is currently on «site» A"
          without the user doing anything,
          the cookie is NOT sent.

          That is a tracking threat, which `SameSite=Lax` was designed to block.

        - Any «site»,
          which is different from «site» B
          and
          which issues an invisible background request to «site» B,
          can't silently trigger an authenticated action on «site» B on the user's behalf.
        
          That is a CSRF threat, which `SameSite=Lax` was designed to block.
    
    on all subsequent requests to «site» B (browsing around, adding to cart, checkout, etc.),
      the browser sends the cookie along automatically;
      «site» B's server
      reads the cookie,
      displays a discount banner,
      credits the affiliate (if the user purchases the discounted product),
      etc.

    example:
    ```
    Set-Cookie: affiliate=e4rt45dw; SameSite=Lax
    ```

  - `None`

    specifies that cookies are sent on both originating and «cross-site requests»

    requires a *secure context*,
    which means that,
    if `SameSite=None` is set then, the `Secure` attribute must also be set

    useful if you want to send cookies along with requests made from third-party content embedded in other sites, for example, ad-tech or analytics providers

    example:
    ```
    Set-Cookie: widget_session=7yjgj57e4n3d; SameSite=None; Secure; HttpOnly
    ```

<br />

---

<br />

Cookie prefixes

> Because of the design of the cookie mechanism, a server can't confirm that a cookie was set from a secure origin or even tell *where* a cookie was originally set.
> 
> An application on a subdomain can set a cookie with the `Domain` attribute, which gives access to that cookie on all other subdomains. This mechanism can be abused in a [session fixation](
>     https://owasp.org/www-community/attacks/Session_fixation
> ) attack.

As a [defense-in-depth measure](
    https://en.wikipedia.org/wiki/Defense_in_depth_(computing)
), you can use *cookie prefixes* to impose specific restrictions on a cookie's attributes in supporting user-agents.
All cookie prefixes start with a double-underscore (`__`) and end in a dash (`-`).
[Several cookie prefixes are available.]

The browser will reject cookies with these prefixes that don't comply with their restrictions. As the application server only checks for a specific cookie name when determining if the user is authenticated or a CSRF token is correct, this effectively acts as a defense measure against [session fixation](
    https://owasp.org/www-community/attacks/Session_fixation
).

- Cookies with names starting with `__Secure-`

- Cookies with names starting with `__Host-`

- Cookies with names starting with `__Http-`

- Cookies with names starting with `__Host-Http-`
