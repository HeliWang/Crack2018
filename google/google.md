### 按下google会发生什么

**1. The browser checks the cache for a DNS record to find the corresponding IP adress.**

* First, it checks the browser cache

* Second, the browser checks the OS cache, if not found, the browser would make a system call \(ie. gethostname on Windows\) to your underlying computer OS to fetch the record since the OS also maintains a cache of DNS recourds.
* Third, it checks the router cache.
* Fourth, it checks the ISP cache.

**2. If the requested URL is not in all the cache, ISP's DNS server initiates a DNS query to find the IP. Those DNS servers are called name servers.**

![](/assets/name_server.png)

For maps.google.com, it will go from root =&gt; .com =&gt; google.com.

**3. Browser initiates a TCP connection with the server**

TCP Three-way handshake

**4. The browser sends an HTTP request to the web server**

GET request ask for web page. If you're entering credentials or submitting form this could be a POST request. This contains browser identification \(User-Agent header\), types of requests that it will accept \(Accept-header\), and Connection header asking it to keep the TCP alive for additional requests5.

**5. The server handles the request and sends back a response**

The server \(Apache, IIS\) which receives the request from the browser and passes it to a request handler to read and generate a response like JSON, XML, HTML.

**6. The server sends out an HTTP response**

The server response contains the web page you requested as well as the status.

Example:

![](/assets/HTTP_response.png)

● 1xx indicates an informational message only

● 2xx indicates success of some kind

● 3xx redirects the client to another URL

● 4xxindicates an error on the client’s part

● 5xx indicates an error on the server’s part

**7. The browser displays the HTML content**

At first, render the bare bone HTML skeleton, then check the HTML tags and sends out GET requests for additional elements on the web page, such as images, CSS stylesheets, JavaScript files etc. These static files are cached by the browser so it doesn’t have to fetch them again the next time you visit the page.

