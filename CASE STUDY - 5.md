# Experiment 5: Analysis of Data Communication in a Web Application Using Browser Developer Tools

## 1. Aim

To analyze how a web application communicates with servers (requests, responses, headers, cookies, timing, and security) using browser developer tools.

## 2. Objectives

- Open and navigate the Network tab of browser DevTools.
- Identify HTTP methods, status codes, headers, and payloads.
- Observe cookies, caching, and compression.
- Measure page load performance.
- Inspect HTTPS/TLS details and WebSocket traffic (optional).

## 3. Requirements

| Item | Details |
|---|---|
| Browser | Google Chrome, Microsoft Edge, or Firefox (steps below use Chrome/Edge naming) |
| Internet access | Required |
| Test sites | Any website you are permitted to inspect, such as `https://example.com`, or a practice API such as `https://jsonplaceholder.typicode.com` |

> Only analyze sites you own or that are intended for public testing. Do not tamper with other people's applications.

## 4. Theory

### 4.1 HTTP Request/Response Model

| Element | Request | Response |
|---|---|---|
| First line | Method, URL, version (e.g., `GET /index.html HTTP/1.1`) | Version, status code, reason (e.g., `HTTP/1.1 200 OK`) |
| Headers | Host, User-Agent, Accept, Cookie, Authorization | Content-Type, Content-Length, Set-Cookie, Cache-Control |
| Body | Optional (POST, PUT) | HTML, JSON, images, scripts, etc. |

### 4.2 Common HTTP Methods

| Method | Purpose |
|---|---|
| GET | Retrieve a resource |
| POST | Submit data to create a resource |
| PUT / PATCH | Replace / partially update a resource |
| DELETE | Remove a resource |
| OPTIONS | Ask which methods are allowed (used in CORS preflight) |

### 4.3 Common Status Codes

| Range | Meaning | Examples |
|---|---|---|
| 1xx | Informational | 101 Switching Protocols (WebSocket) |
| 2xx | Success | 200 OK, 201 Created, 204 No Content |
| 3xx | Redirection | 301 Moved Permanently, 302 Found, 304 Not Modified |
| 4xx | Client error | 400 Bad Request, 401 Unauthorized, 403 Forbidden, 404 Not Found |
| 5xx | Server error | 500 Internal Server Error, 503 Service Unavailable |

## 5. Procedure

### Part A: Open DevTools and Record Traffic

1. Open the browser and press **F12** (or **Ctrl+Shift+I**; **Cmd+Option+I** on macOS).
2. Select the **Network** tab.
3. Tick **Preserve log** and **Disable cache** (for the first run).
4. Navigate to `https://example.com` and wait for the page to load.
5. Observe the request list: each row is one request (name, status, type, size, time).

### Part B: Inspect a Single Request

1. Click the first request (the HTML document).
2. Open the **Headers** panel and record:
   - Request URL, method, status code, remote address
   - Request headers (Host, User-Agent, Accept, Accept-Encoding)
   - Response headers (Content-Type, Content-Encoding, Cache-Control, Server, Date)
3. Open **Preview** and **Response** to view the returned content.
4. Open **Timing** to view the breakdown: queueing, DNS lookup, initial connection, SSL, request sent, waiting (TTFB), and content download.

### Part C: Filter and Analyze Resources

1. Use the filter buttons (Fetch/XHR, JS, CSS, Img, Doc) to view requests by type.
2. Sort by **Size** and **Time** to find the largest and slowest resources.
3. Check the status bar at the bottom for total requests, transferred size, and **DOMContentLoaded** and **Load** times.

### Part D: Observe API Calls (GET and POST)

1. Open the console (**Console** tab) while on any page, and run:

```javascript
// GET request
fetch('https://jsonplaceholder.typicode.com/posts/1')
  .then(r => r.json())
  .then(console.log);

// POST request
fetch('https://jsonplaceholder.typicode.com/posts', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ title: 'test', body: 'hello', userId: 1 })
})
  .then(r => r.json())
  .then(console.log);
```

2. In the Network tab, filter **Fetch/XHR**.
3. Select each request and note the method, status code (200 and 201), request payload (Payload tab), and JSON response.

### Part E: Cookies and Storage

1. Visit a site that sets cookies (any site with a login or consent banner).
2. In a response, find the `Set-Cookie` header.
3. Open **Application** tab > **Cookies** and record name, value, domain, path, expiry, `Secure`, `HttpOnly`, and `SameSite` flags.
4. Also check **Local Storage** and **Session Storage**.

### Part F: Caching Behavior

1. Clear **Disable cache**.
2. Reload the page normally, then reload again.
3. Look for requests with status **304 Not Modified** or size shown as **(memory cache)** / **(disk cache)**.
4. Note related headers: `Cache-Control`, `ETag`, `Last-Modified`.

### Part G: HTTPS and Security

1. Click the padlock icon in the address bar > connection details/certificate.
2. Record issuer, validity dates, and protocol version.
3. Open the **Security** panel (if available) or inspect headers such as `Strict-Transport-Security`, `Content-Security-Policy`, `X-Content-Type-Options`.

### Part H: Throttling and Offline Behavior (Optional)

1. In the Network tab, change **No throttling** to **Slow 3G** or **Fast 3G**.
2. Reload and compare load times with the earlier measurement.

### Part I: WebSocket Traffic (Optional)

1. Visit a site that uses WebSockets or open a WebSocket echo demo you are allowed to use.
2. Filter by **WS** and open the **Messages** tab to observe frames sent and received.

## 6. Observations

### Main Document Request

| Item | Value |
|---|---|
| URL | |
| Method | |
| Status code | |
| Protocol (HTTP/1.1, h2, h3) | |
| Content-Type | |
| Content-Encoding | |
| Server | |

### Page Load Summary

| Metric | Value |
|---|---|
| Total requests | |
| Total transferred size | |
| DOMContentLoaded (ms) | |
| Load (ms) | |
| Slowest resource | |
| Largest resource | |

### Timing Breakdown (Main Request)

| Phase | Time (ms) |
|---|---|
| DNS lookup | |
| Initial connection | |
| SSL | |
| Waiting (TTFB) | |
| Content download | |

### API Calls

| Request | Method | Status | Payload Sent | Response Summary |
|---|---|---|---|---|
| /posts/1 | GET | | None | |
| /posts | POST | | | |

### Cookie Record

| Name | Domain | Expiry | Secure | HttpOnly | SameSite |
|---|---|---|---|---|---|
| | | | | | |

## 7. Result

Browser developer tools were used to analyze HTTP communication, including request and response headers, status codes, payloads, cookies, caching, timing, and security information of a web application.

## 8. Conclusion

The Network tab gives a clear view of how browsers and servers exchange data. It helps diagnose performance problems, debug API calls, verify security headers, and understand how protocols such as HTTP, TLS, and WebSocket work in practice.

## 9. Viva Questions

1. What is the difference between GET and POST?
2. What does status code 304 mean?
3. What is TTFB and why does it matter?
4. What do the `HttpOnly` and `Secure` cookie flags do?
5. How does HTTP/2 differ from HTTP/1.1?
6. What is CORS and when does a preflight (OPTIONS) request occur?
