# Web Application Basics

# HTTP Request Headers

In web applications, **headers** are pieces of metadata sent along with HTTP requests and responses. They provide information about the request, the response, the client, the server, authentication, content type, and more.

When a browser sends a request to a server:

```
GET /users HTTP/1.1
Host: example.com
User-Agent: Chrome/137
Accept: application/json
Authorization: Bearer abc123
```


When the server responds:

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 125
Cache-Control: no-cache

{
  "name": "John"
}
```


## Accept

```
Accept: text/html, application/json
```

The client can process responses in either **HTML** (`text/html`) or **JSON** (`application/json`) format.


## Authorization

An HTTP request header used to send credentials or tokens that identify and authenticate the client to the server.

```
Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQ=
```

Here:

1. Username and password are combined:

```
username:password
```

2. The string is Base64 encoded:

```
dXNlcm5hbWU6cGFzc3dvcmQ=
```

3. Sent to the server in the `Authorization` header.

## Cache-Control 

**`Cache-Control`** is an HTTP header that provides directives for caching mechanisms, specifying how browsers, proxies, CDNs, and other caches should store, reuse, and validate HTTP responses.

```
Cache-Control: no-cache
```

To control whether cached content can be used or whether the client must check with the server for a fresh version.

##### Why Caching Exists

Imagine a user visits a website:

```
Browser → Server → Response
```

Every time the user refreshes the page, the browser would need to download everything again.

This causes:

- More server load
- Slower websites
- More bandwidth usage

To solve this, browsers store copies of resources (HTML, CSS, JS, images) in a **cache**.

```
First Visit:
Browser → Server → Response → Cache

Second Visit:
Browser → Cache → Display
```

This makes websites much faster.

## Cookie

An HTTP request header that contains cookies previously sent by the server and stored by the client's browser.

```
Cookie: sessionId=abc123
```

To maintain user state, sessions, preferences, and authentication across multiple HTTP requests.

Cookies are automatically sent by the browser with every matching request to the website that set them, provided the cookie has not expired and its domain, path, Secure, and SameSite restrictions allow it to be included.

##### Why Cookies Exist (Simple Points)

- HTTP is **stateless**, meaning the server does not remember previous requests.
- Cookies help the server **identify and remember users** between requests.
- They allow users to **stay logged in** without entering credentials on every page.
- They help websites **maintain sessions**.
- They store **user preferences** such as language, theme, and settings.
- They help manage **shopping carts** in e-commerce websites.
- They enable **personalized content** and recommendations.
- They can be used for **analytics and user tracking**.

## Content-Type 

An HTTP header that specifies the **format (media type) of the data** being sent in the request or response body.

```
Content-Type: application/json
```

**Request:**

```
POST /login HTTP/1.1
Content-Type: application/json

{
  "username": "kapil",
  "password": "pass123"
}
```


Common Content Types

|Content-Type|Meaning|
|---|---|
|`text/html`|HTML page|
|`application/json`|JSON data|
|`text/plain`|Plain text|
|`application/xml`|XML data|
|`application/x-www-form-urlencoded`|Form data|
|`multipart/form-data`|File uploads|

## Host Header

An HTTP request header that specifies the **domain name (and optionally the port number)** of the server the client wants to access.

```
Host: example.com
```

To tell the server which website or virtual host the client is requesting.

```
GET /index.html HTTP/1.1
Host: example.com
```

A single server can host multiple websites:

```
Server IP: 192.168.1.10

example.com
blog.example.com
shop.example.com
```

The `Host` header tells the server which website the client wants.

## User-Agent

`User-Agent` is an HTTP request header that identifies the client application, browser, operating system, or device making the request, allowing the server to provide compatible content and gather usage information.

The `User-Agent` header tells the server:

- "Who am I? Which browser, operating system, or application is sending this request?"

```
User-Agent: Mozilla/5.0 Chrome/137.0
```

## Referer Header
  
**`Referer`** is an HTTP request header that tells the server **which webpage the user was on before making the current request**.

```
Referer: https://example.com/login
```

#### Why Does Referer Exist?

When a user clicks a link, submits a form, or loads an image/script, the server may want to know:

- Where the user came from
- Which page generated the request
- Whether the request is legitimate

#### Basic Example

Step 1: User visits Home Page

```
https://shop.com/home
```

The page contains a link:

```
<a href="/products">Products</a>
```

 Step 2: User clicks the link

Browser sends:

```
GET /products HTTP/1.1Host: shop.comReferer: https://shop.com/home
```

**What the Server Sees**

```
Current Request:    
	/products

User Came From:    
	/home
```

The server knows the user navigated from the Home page.

## X-Forwarded-For (XFF)

An HTTP header used to identify the original IP address of a client when the request passes through one or more proxies, load balancers, or reverse proxies.

```
X-Forwarded-For: 203.0.113.10
```

---
# HTTP Response Headers

## Content-Type (Response Header)

A response header that tells the browser **what type of data the server is sending in the response body**.

```
Content-Type: text/html
```

## Content-Length

A response header that specifies the **size of the response body in bytes**.

```
Content-Length: 125
```

To tell the client (browser) how much data is being sent in the response.

```
HTTP/1.1 200 OK
Content-Type: text/html
Content-Length: 31

<h1>Hello World</h1>
```

## Server Header

`Server` is an HTTP response header that identifies the web server software handling the request.

```
Server: Apache/2.4.58
```

To tell the client which web server software generated the response.

```
HTTP/1.1 200 OK
Server: nginx/1.28.0
Content-Type: text/html
```

## ETag

**ETag (Entity Tag)** is an HTTP response header that acts as a **unique identifier (fingerprint)** for a specific version of a resource (HTML page, CSS file, image, JavaScript file, API response, etc.).

```
ETag: "3f80f-1b6-3ec4gy603b"
```

## Strict-Transport-Security (HSTS)

**`Strict-Transport-Security` (HSTS)** is an HTTP response security header that instructs browsers to communicate with a website **only over HTTPS** and never over insecure HTTP for a specified period.

```
Strict-Transport-Security: max-age=31536000
```

#### Why Does HSTS Exist?

Normally, a user might type:

```
http://example.com
```

The browser first connects using HTTP and then gets redirected to HTTPS.

```
HTTP
 ↓
Redirect
 ↓
HTTPS
```

This initial HTTP connection can be intercepted by an attacker.

# Security Headers

## Content-Security-Policy (CSP)

**`Content-Security-Policy` (CSP)** is an HTTP security response header that tells the browser **which sources of content (scripts, styles, images, frames, etc.) are allowed to load and execute on a webpage**.

```
Content-Security-Policy: default-src 'self'
```

To prevent attacks such as:

- Cross-Site Scripting (XSS)
- Data injection attacks
- Malicious script execution

Imagine your website is a house.

Without CSP:

```
Anyone can enter the house.
```

With CSP:

```
Only approved people can enter.
```

## X-Content-Type-Options

**`X-Content-Type-Options`** is an HTTP security response header that prevents browsers from performing **MIME type sniffing** and forces them to strictly follow the `Content-Type` header specified by the server.

```
X-Content-Type-Options: nosniff
```

To prevent browsers from incorrectly interpreting files and potentially executing malicious content.

#### Example 

Server sends:

```
Content-Type: text/plain
```

Without `nosniff`:

```
Browser:"This looks like JavaScript."
↓
Execute it
```

With:

```
X-Content-Type-Options: nosniff
```

Browser:

```
Server says text/plain
↓
Treat as plain text only
↓
Do not execute
```

## X-XSS-Protection

**`X-XSS-Protection`** is an HTTP security response header that enables or disables the browser's built-in **Cross-Site Scripting (XSS) filter**.

```
X-XSS-Protection: 1; mode=block
```

```
Enable XSS filter.
If XSS is detected,
block the page completely.
```

## Referrer-Policy Header

**`Referrer-Policy`** is an HTTP security response header that controls how much referrer information the browser sends in the `Referer` header when navigating to another page or website.

```
Referrer-Policy: strict-origin-when-cross-origin
```

To prevent sensitive information from being leaked through the `Referer` header while still allowing useful analytics and navigation tracking.

---
# What is same-origin policy (SOP)?

The **Same-Origin Policy (SOP)** is a **browser security mechanism** that restricts how documents or scripts loaded from one **origin** can interact with resources from another origin. An **origin** is defined by the combination of **protocol (scheme)**, **host (domain)**, and **port**.

## Origin

An **origin** consists of:

- Protocol
- Domain 
- Port
 
|Component|Value|
|---|---|
|Protocol|https|
|Domain|example.com|
|Port|443|

#### Scenario

User is logged into:

```
https://bank.com
```

and has a valid session:

```
sessionId=abc123
```

Now the user visits:

```
https://evil.com
```

The attacker tries to steal bank data using JavaScript:

```
fetch("https://bank.com/account")
  .then(response => response.text())
  .then(data => console.log(data));
```

#### What Happens?

Browser checks the origins:

```
Current Website: https://evil.com
Target Website:  https://bank.com
```

Comparison:

|Component|evil.com|bank.com|Same?|
|---|---|---|---|
|Protocol|https|https|✓|
|Domain|evil.com|bank.com|✗|
|Port|443|443|✓|

Since the **domain is different**, the origins are different.

Result:

```
Same-Origin Policy blocks evil.com
from reading the response from bank.com.
```

#### Why SOP Is Important

Without SOP:

```
evil.com
↓
Read bank account details
↓
Steal sensitive information
```

With SOP:

```
evil.com
↓
Request may be sent
↓
Response cannot be read
↓
Data remains protected
```


# What is CORS (Cross-Origin Resource Sharing)?

**CORS (Cross-Origin Resource Sharing)** is a browser security mechanism that allows a website to access resources from a different origin if the target server allows the request.

To safely bypass the restrictions imposed by the **Same-Origin Policy (SOP)**.

### Why CORS Exists

#### Same-Origin Policy (SOP)

Suppose your frontend is hosted at:

```
https://app.example.com
```

and it tries to fetch data from:

```
https://api.example.com
```

JavaScript:

```
fetch("https://api.example.com/users")
```

Browser checks:

|Component|app.example.com|api.example.com|
|---|---|---|
|Protocol|https|https|
|Domain|app.example.com|api.example.com|
|Port|443|443|

Different domain = Different Origin

Result:

```
Blocked by SOP
```

### Solution: CORS

The API server can explicitly allow access.

Server response:

```
Access-Control-Allow-Origin: https://app.example.com
```

Browser sees:

```
Server trusts app.example.com
```

Result:

```
Request Allowed
```

## Difference Between SOP and CORS

|SOP|CORS|
|---|---|
|**Same-Origin Policy**|**Cross-Origin Resource Sharing**|
|Browser security mechanism|Mechanism to relax SOP restrictions|
|Blocks cross-origin access by default|Allows controlled cross-origin access|
|Protects users from malicious websites|Allows trusted websites to access resources|
|Enforced by browser automatically|Configured by the server using HTTP headers|
|No server configuration required|Requires CORS headers from the server|

### 1. Cross-Origin-Embedder-Policy (COEP)

**Cross-Origin-Embedder-Policy (COEP)** is a browser security policy that controls which resources (images, scripts, videos, iframes, etc.) from other websites can be loaded into your webpage.

Blocks loading of cross-origin resources unless explicitly allowed, enhancing security from  embedded resources.
- Does nothing unless enabled by the website

```
Cross-Origin-Embedder-Policy: require-corp
```

- Prevents unauthorized cross-origin resource loading.
- Enables stronger browser isolation.
- Helps protect against data leakage and side-channel attacks.

### 2. Cross-Origin-Opener-Policy (COOP)

**Cross-Origin-Opener-Policy (COOP)** isolates your webpage from other websites that are opened in windows, new tabs or popups.

```
Cross-Origin-Opener-Policy: same-origin
```

- Prevents cross-origin window attacks.
- Stops malicious sites from interacting with your tab.
- Creates a separate browsing context.

### 3. Cross-Origin-Resource-Policy (CORP)

**Cross-Origin-Resource-Policy (CORP)** is a security header that tells browsers which websites are allowed to load or use a resource.

CORP lets the resource owner decide who can use their resource.

```
Cross-Origin-Resource-Policy: same-origin
Cross-Origin-Resource-Policy: same-site
Cross-Origin-Resource-Policy: cross-origin
```

**Example:**

Suppose your website hosts an image:

```
https://mywebsite.com/logo.png
```

Another website tries to load it:

```
<img src="https://mywebsite.com/logo.png">
```

Without CORP, any website might be able to load that image.

With CORP, the resource owner can decide:

- Only my website can use it
- Only websites from my domain can use it
- Any website can use it

### 4. Permissions-Policy

**Permissions-Policy** lets a website decide which browser features (camera, microphone, geolocation, fullscreen, etc.) and APIs can be used by itself or by embedded content like iframes.

```
Permissions-Policy: geoloaction=(self), camera=(), microphone=()
```

### 5. Expect-CT

**Expect-CT** is a security header that tells browsers to verify that a website's TLS/SSL certificate is properly logged in Certificate Transparency (CT) logs.

Expect-CT helps detect fake or unauthorized SSL certificates.

```
Expect-CT: max-age=86400, enforce
```

- Detects fraudulent certificates.
- Prevents misuse of SSL/TLS certificates.
- Improves HTTPS trust.

## Content-Security-Policy (CSP)

The **Content-Security-Policy (CSP)** is powerful security header that tells browser which content (scripts, images, CSS, fonts, etc.) is allowed to load on a webpage.

It is a powerful tool to mitigate attacks such as Cross-Site-Scripting (XSS), clickjacking, and other code injection attacks. It allows you to control which resources are loaded by web application.

```
Content-Security-Policy: default-src 'self';
```

```
Content-Security-Policy:
default-src 'self';
script-src 'self' 'unsafe-inline' 'unsafe-eval' https://apis.google.com;
style-src 'self' 'unsafe-inline' https://fonts.googleapis.com;
font-src 'self' https://fonts.gstatic.com;
img-src 'self' data: https://cdn.example.com;
connect-src 'self' https://api.example.com https://socket.example.com;
media-src 'self';
object-src 'none';
frame-ancestors 'self';
form-action 'self';
base-uri 'self';
upgrade-insecure-requests;
block-all-mixed-content;
```


```
Explanation of Values:

1. default-src 'self';

   Specifies that only resources from the same origin ('self')
   are allowed by default.

2. script-src 'self' 'unsafe-inline' 'unsafe-eval'
   https://apis.google.com;

   Allows JavaScript from the same origin, inline scripts,
   eval() functions, and scripts from Google's APIs.

3. style-src 'self' 'unsafe-inline'
   https://fonts.googleapis.com;

   Allows styles from the same origin, inline styles,
   and Google Fonts. Inline styles should be avoided
   where possible.

4. font-src 'self' https://fonts.gstatic.com;

   Allows fonts to load from the same origin and
   Google's font CDN.

5. img-src 'self' data: https://cdn.example.com;

   Allows images from the same origin, base64-encoded
   inline images (data:), and a specific CDN.

6. connect-src 'self' https://api.example.com
   https://socket.example.com;

   Defines allowed sources for AJAX requests,
   WebSocket connections, and EventSource connections.

7. media-src 'self';

   Restricts the origin of media (audio and video)
   resources to the same origin.

8. object-src 'none';

   Prevents the use of <object>, <embed>, and <applet>
   elements, which are often vectors for attacks.

9. frame-ancestors 'self';

   Ensures that other domains cannot embed the site
   in an iframe, mitigating clickjacking attacks.

10. form-action 'self';

    Limits the destinations to which forms can submit
    data to the same origin.

11. base-uri 'self';

    Restricts the URLs used in the <base> element
    to the same origin.

12. upgrade-insecure-requests;

    Automatically upgrades HTTP requests to HTTPS
    to ensure secure communication.

13. block-all-mixed-content;

    Blocks any mixed content
    (e.g., HTTP resources on an HTTPS page).
```

##### CSP Evaluator

**CSP Evaluator** is a tool that analyzes a Content Security Policy (CSP) and checks whether it contains security weaknesses or misconfigurations.

```
Link: https://csp-evaluator.withgoogle.com/
```


## X-Frame-Options

**`X-Frame-Options`** is an HTTP security response header that controls whether a webpage can be displayed inside a frame (`<frame>`), iframe (`<iframe>`), or object (`<object>`).

To protect websites from **Clickjacking attacks** by preventing unauthorized websites from embedding the page inside a frame.


```
X-Frame-Options: DENY
```

Prevents the webpage from being displayed inside **any** `<iframe>` or `<frame>`, regardless of the origin.


```
X-Frame-Options: SAMEORIGIN
```

Allows the webpage to be displayed inside an iframe **only if the parent page belongs to the same origin (same protocol, domain, and port).**


```
X-Frame-Options: ALLOW-FROM https://trusted-partner.com
```

Allows the webpage to be displayed inside an iframe only on the specified trusted website.


## X-XSS-Protection

**`X-XSS-Protection`** is an HTTP security response header that was used to enable or disable the browser's built-in **Cross-Site Scripting (XSS) protection mechanism**. It helped detect and block some reflected XSS attacks in older browsers.

*This header is **deprecated** and is no longer recommended because modern browsers have removed support for it or replaced it with stronger protections like **Content-Security-Policy (CSP)**.*

##### Values and Their Definitions

```
X-XSS-Protection: 0
```

Disables the browser's built-in XSS protection mechanism.


```
X-XSS-Protection: 1
```

Enables the browser's built-in XSS protection mechanism. If the browser detects a XSS attack, it attempts to sanitize (remove) the malicious script and continue loading the page.


```
X-XSS-Protection: 1; mode=block
```

Enables the browser's built-in XSS protection mechanism. If an XSS attack is detected, the browser blocks the entire webpage instead of trying to sanitize it.


```
X-XSS-Protection: 1; report=https://example.com/report
```

Enables the browser's built-in XSS filter and instructs the browser to send a report to the specified URL if an XSS attack is detected.

This directive was not widely supported by browsers and is now deprecated, just like the `X-XSS-Protection` header itself.