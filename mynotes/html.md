## ❖ Hypertext Markup Language (HTML)

### 1. **What is HTML?**

**HTML (HyperText Markup Language)** is the standard markup language used to create and structure content on the web. It defines the structure and layout of a web document using a system of **elements** represented by tags like `<p>`, `<a>`, `<div>`, etc.

HTML describes **what** elements on a page are — for example:

* Headings (`<h1>`)
* Paragraphs (`<p>`)
* Links (`<a>`)
* Images (`<img>`)

However, HTML does **not handle styling** or behavior — that’s done using **CSS** and **JavaScript** respectively.

**Follow-up Questions:**

* What is the difference between HTML and XML?
* Can a web page function without HTML?

---

### 2. **Describe the meaning of the word "Hyper"**

The word **"Hyper"** in **HyperText** means *non-linear*. Traditional text follows a linear path (like reading a book), but **HyperText allows you to jump to any other piece of text via links**. This is the core idea behind navigating the web using hyperlinks (`<a href="">`).

**Follow-up Questions:**

* Who coined the term HyperText?
* How does HyperText differ from normal text?

---

### 3. **Give a brief introduction about HTML history**

HTML was created by **Tim Berners-Lee** in **1991** while working at CERN. It started as a basic language for sharing documents across the internet.

**Milestones:**

* **HTML 1.0** – Basic text, images, and links.
* **HTML 2.0 (1995)** – Formal specification with forms and tables.
* **HTML 3.2 & 4.01 (1997-1999)** – Support for CSS and scripting.
* **XHTML (2000)** – A stricter version of HTML using XML syntax.
* **HTML5 (2014)** – Major update adding audio, video, semantic elements, canvas, and APIs.

**Follow-up Questions:**

* What’s the difference between HTML4 and HTML5?
* What is the W3C and WHATWG?

---

### 4. **What is an IP address?**

An **IP address** (Internet Protocol address) is a unique numerical identifier assigned to every device connected to the internet or a local network.

Types:

* **IPv4**: 32-bit (e.g., 192.168.0.1)
* **IPv6**: 128-bit (e.g., 2001:0db8:85a3:0000:0000:8a2e:0370:7334)

It’s like your home address, but for internet-connected devices.

**Follow-up Questions:**

* How does a domain name relate to an IP address?
* What’s the difference between static and dynamic IP?

---

### 5. **Why was IPv6 introduced?**

IPv6 was introduced to solve **IPv4 address exhaustion**. IPv4 can support around **4.3 billion devices**, but with the rise of IoT, smartphones, etc., this was not enough.

**Benefits of IPv6:**

* Vast address space (2^128 addresses)
* Better security (IPsec built-in)
* Efficient routing and packet processing

**Follow-up Questions:**

* Can IPv4 and IPv6 coexist?
* What is NAT and how did it help delay IPv6?

---

### 6. **Explain the process of a web server and why do we need it**

A **web server** is a system (hardware + software) that **stores, processes, and delivers web pages** to users upon request.

**Process:**

1. A browser sends an HTTP request for a web page.
2. The web server receives the request and fetches the required HTML/CSS/JS files.
3. It sends these files back to the browser using HTTP/HTTPS.
4. The browser renders the content.

**Why we need it:**

* Central hosting of files
* Handles multiple users
* Security and performance features

**Follow-up Questions:**

* What is Apache/Nginx?
* What is the difference between a web server and an application server?

---

### 7. **What is a web browser?**

A **web browser** is a software application that **retrieves and displays content from web servers**. Examples: Chrome, Firefox, Safari, Edge.

It:

* Sends HTTP requests
* Interprets HTML, CSS, and JS
* Renders the content visually

**Follow-up Questions:**

* How does a browser engine work?
* What is the role of a user agent?

---

### 8. **How HTTP works and what does it really do?**

**HTTP (HyperText Transfer Protocol)** is the protocol for **communication between browsers and web servers**.

**Process:**

1. The browser sends an HTTP request (GET, POST, etc.)
2. The server processes the request and sends an HTTP response.
3. This includes a status code (e.g., 200 OK, 404 Not Found) and content.
4. HTTP is stateless — each request is independent.

**Follow-up Questions:**

* What’s the difference between HTTP and HTTPS?
* What are common HTTP methods and status codes?

---

### 9. **What are the element function groups that we use in HTML?**

HTML elements are functionally grouped as:

* **Structural**: `<div>`, `<header>`, `<section>`, `<footer>`
* **Text content**: `<h1>`–`<h6>`, `<p>`, `<span>`, `<blockquote>`
* **Forms**: `<form>`, `<input>`, `<textarea>`, `<select>`
* **Embedded content**: `<img>`, `<audio>`, `<video>`, `<iframe>`
* **Scripting**: `<script>`, `<noscript>`
* **Metadata**: `<title>`, `<meta>`, `<link>`

**Follow-up Questions:**

* What are semantic elements?
* What are void elements?

---

### 10. **Describe the anatomy of an HTML element**

A typical HTML element includes:

```html
<p class="intro">This is a paragraph.</p>
```

* **Start tag**: `<p>`
* **Attributes**: `class="intro"`
* **Content**: `This is a paragraph.`
* **End tag**: `</p>`

**Follow-up Questions:**

* What are self-closing tags?
* Can attributes have boolean values?

---

### 11. **Describe the main strategies that we use for web designing**

Web design strategies focus on:

* **Responsive design** (adapts to screen sizes)
* **Mobile-first design**
* **Grid and Flexbox layout systems**
* **Accessibility (a11y)**
* **Performance optimization (lazy loading, compression)**
* **SEO (Search Engine Optimization)**

**Follow-up Questions:**

* What is the difference between adaptive and responsive design?
* What is progressive enhancement?

---

### 12. **What are meta tags and why do we want them in HTML?**

Meta tags provide **metadata** about the HTML document, such as:

* Character set: `<meta charset="UTF-8">`
* Description: `<meta name="description" content="...">`
* Viewport settings: `<meta name="viewport" content="width=device-width, initial-scale=1.0">`

They help with:

* SEO
* Browser behavior
* Social sharing (Open Graph)

**Follow-up Questions:**

* Do meta tags affect performance?
* What are Open Graph meta tags?

---

### 13. **What is a domain name?**

A domain name is a **human-readable address** used to identify a website on the internet (e.g., `example.com`). It maps to an IP address via DNS.

**Parts:**

* **Top-level domain (TLD)**: `.com`, `.org`
* **Second-level domain**: `example`
* **Subdomain**: `blog.example.com`

**Follow-up Questions:**

* How is a domain registered?
* What is a premium domain?

---

### 14. **What is DNS?**

**DNS (Domain Name System)** is the internet's phonebook. It **translates domain names into IP addresses**.

Process:

1. You type `www.google.com`
2. DNS resolves it to `142.250.190.4`
3. Browser uses the IP to make the request

**Follow-up Questions:**

* What is DNS caching?
* What is a DNS record (A, MX, CNAME)?

---

### 15. **What is a URL? What parts does it contain?**

**URL (Uniform Resource Locator)** is the complete web address to access a resource.

Example:

```
https://www.example.com:443/path/page.html?search=html#section1
```

**Parts:**

* **Protocol**: `https://`
* **Subdomain**: `www.`
* **Domain**: `example.com`
* **Port**: `443`
* **Path**: `/path/page.html`
* **Query string**: `?search=html`
* **Fragment**: `#section1`

**Follow-up Questions:**

* What’s the difference between URI and URL?
* How does a query string affect server behavior?

---

### 16. **What are HTML attributes?**

Attributes provide **additional information** about elements. They are placed inside the start tag.

Example:

```html
<img src="image.jpg" alt="A sample image" width="300">
```

Common attributes: `id`, `class`, `src`, `href`, `alt`, `title`, `style`

**Follow-up Questions:**

* What are global attributes?
* What is the difference between `id` and `class`?

---

### 17. **What is the usage of HTML `<!DOCTYPE html>` preamble?**

This declaration tells the browser the version of HTML being used. For modern websites:

```html
<!DOCTYPE html>
```

It triggers **standards mode** in browsers, ensuring consistent behavior.

**Follow-up Questions:**

* What happens if we omit the DOCTYPE?
* Is DOCTYPE case-sensitive?

---
