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
# What is same-origin policy?

The **Same-Origin Policy (SOP)** is a **browser security mechanism** that restricts how documents or scripts loaded from one **origin** can interact with resources from another origin. An **origin** is defined by the combination of **protocol (scheme)**, **host (domain)**, and **port**.