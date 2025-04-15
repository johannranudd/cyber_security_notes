[[web applications]]

### security headers
scan / analyse website security headers: https://securityheaders.com/


### Content-Security-Policy:

``Content-Security-Policy: default-src 'self'; script-src 'self' https://cdn.tryhackme.com; style-src 'self'``

 default-src
- which specifies the default policy of self, which means only the current website.

script-src
- which specifics the policy for where scripts can be loaded from, which is self along with scripts hosted on https://cdn.tryhackme.com

style-src
- which specifies the policy for where style CSS style sheets can be loaded from the current website (self)

Strict-Transport-Security (HSTS)

The HSTS header ensures that web browsers will always connect over HTTPS. Let's look at an example of HSTS:




### Strict-Transport-Security: max-age=63072000; includeSubDomains; preload


Here’s a breakdown of the example HSTS header by directive:

    max-age
    - This is the expiry time in seconds for this setting

    includeSubDomains
    - An optional setting that instructs the browser to also apply this setting to all subdomains.

    preload
    - This optional setting allows the website to be included in preload lists. Browsers can use preload lists to enforce HSTS before even having their first visit to a website.




X-Content-Type-Options

The X-Content-Type-Options header can be used to instruct browsers not to guess the MIME time of a resource but only use the Content-Type header. Here’s an example:




### X-Content-Type-Options: nosniff

Here’s a breakdown of the X-Content-Type-Options header by directives:

    nosniff
    - This directive instructs the browser not to sniff or guess the MIME type.

Referrer-Policy

This header controls the amount of information sent to the destination web server when a user is redirected from the source web server, such as when they click a hyperlink. The header is available to allow a web administrator to control what information is shared.  Here are some examples of Referrer-Policy:

    Referrer-Policy: no-referrer
    Referrer-Policy: same-origin
    Referrer-Policy: strict-origin
    Referrer-Policy: strict-origin-when-cross-origin

Here’s a breakdown of the Referrer-Policy header by directives:

    no-referrer
    - This completely disables any information being sent about the referrer

    same-origin
    - This policy will only send referrer information when the destination is part of the same origin. This is helpful when you want referrer information passed when hyperlinks are within the same website but not outside to external websites.

    strict-origin
    - This policy only sends the referrer as the origin when the protocol stays the same. So, a referrer is sent when an HTTPS connection goes to another HTTPS connection.

    strict-origin-when-cross-origin
    - This is similar to strict-origin except for same-origin requests, where it sends the full URL path in the origin header.







---------------------------------------------

### methods

HTTP Methods

The HTTP method tells the server what action the user wants to perform on the resource identified by the URL path. Here are some of the most common methods and their possible security issue:

GET
Used to fetch data from the server without making any changes. Reminder! Make sure you’re only exposing data the user is allowed to see. Avoid putting sensitive info like tokens or passwords in GET requests since they can show up as plaintext.

POST
Sends data to the server, usually to create or update something. Reminder! Always validate and clean the input to avoid attacks like SQL injection or XSS.

PUT
Replaces or updates something on the server. Reminder! Make sure the user is authorised to make changes before accepting the request.

DELETE
Removes something from the server. Reminder! Just like with PUT, make sure only authorised users can delete resources.

Besides these common methods, there are a few others used in specific cases:

PATCH
Updates part of a resource. It’s useful for making small changes without replacing the whole thing, but always validate the data to avoid inconsistencies.

HEAD
Works like GET but only retrieves headers, not the full content. It’s handy for checking metadata without downloading the full response.

OPTIONS
Tells you what methods are available for a specific resource, helping clients understand what they can do with the server.

TRACE
Similar to OPTIONS, it shows which methods are allowed, often for debugging. Many servers disable it for security reasons.

CONNECT
Used to create a secure connection, like for HTTPS. It’s not as common but is critical for encrypted communication.

### Status Codes and Reason Phrases

The Status Code is the number that tells you if the request succeeded or failed, while the Reason Phrase explains what happened. These codes fall into five main categories:

Informational Responses (100-199)
These codes mean the server has received part of the request and is waiting for the rest. It’s a "keep going" signal.

Successful Responses (200-299)
These codes mean everything worked as expected. The server processed the request and sent back the requested data.

Redirection Messages (300-399)
These codes tell you that the resource you requested has moved to a different location, usually providing the new URL.

Client Error Responses (400-499)
These codes indicate a problem with the request. Maybe the URL is wrong, or you’re missing some required info, like authentication.

Server Error Responses (500-599)
These codes mean the server encountered an error while trying to fulfil the request. These are usually server-side issues and not the client’s fault.
Common Status Codes

##### Here are some of the most frequently seen status codes:

100 (Continue)
The server got the first part of the request and is ready for the rest.

200 (OK)
The request was successful, and the server is sending back the requested resource.

301 (Moved Permanently)
The resource you’re requesting has been permanently moved to a new URL. Use the new URL from now on.

404 (Not Found)
The server couldn’t find the resource at the given URL. Double-check that you’ve got the right address.

500 (Internal Server Error)
Something went wrong on the server’s end, and it couldn’t process your request.


