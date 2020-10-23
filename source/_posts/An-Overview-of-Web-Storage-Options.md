---
title: An Overview of Web Storage Options
date: 2019-05-04 09:20:47
intro: Web Storage, IndexedDB, Cache, and Cookies.
featured_image:
tags: 
    - Front-end
---

<img src="web-storage-options.png" width="200px">

⚠️ Web SQL and Application Cache are deprecated.
<br/>

**Modern Storage APIs:**
- Web Storage API
    - A mechanism by which browsers can securely store key/value pairs.
    - Local Storage
        - Provides a permanent storage.
        - Basic usage:
            - `localStorage.setItem('key', 'value');`
            - `localStorage.getItem('key');`
    - Session Storage
        - Maintains data on page sessions. Opening a page in a new tab or window will initiate a new page session, hence having different Session Storage instances for the same site. The page session survives over page reloads and restores until you close the browser. 
        - Basic usage:
            - `sessionStorage.setItem('key', 'value');`
            - `sessionStorage.getItem('key');`
- IndexedDB
    - A low-level API for client-side storage of significant amounts of structured data, including files/blobs. 
<br/>
--- 
**Other Options:**
- Cookies
    - A small piece of data from server and sent back to server with every request from client, typically used to identify if two requests came from the same browser. It’s a stateful solution on stateless HTTP protocol. 
    - Session Cookies
        - Expires when you close the browser.
    - Permanent Cookies
        - Expires at a specific date (`Expires`) or after a specific length of time (`Max-Age`)
    - Basic usage:
        - `Set-Cookie: <name>=<value>` in response header: 
        
            ```
            HTTP/2.0 200 OK
            Content-type: text/html
            Set-Cookie: sessionid=c270e9a6
            Set-Cookie: csrftoken=juILC73NMNnGq

            [page content]
            ```
        - Now every new request sent from client will include a `Cookie` header:

            ```
            GET /sample_page.html HTTP/2.0
            Host: www.example.org
            Cookie: sessionid=a270e9a6; csrftoken=juILC73NMNnGq
            ```
- Cache API
    - A system for storing and retrieving network requests and corresponding responses. It was created to enable Service Workers to cache network requests in order to provide appropriate responses while offline. However, it can also be used for storage purposes as it can save blobs, jsons, form data objects, and etc as `Response` objects. 
    - Basic usage:
        - Feature Detection: `const cacheAvailable = 'caches' in self;`
<br/>
---
**Side Note:**
- Service Worker
    - A proxy that sits between web applications, the browser, and the network (when available). In order to create an effective offline experiences, they intercept network requests, cache responses, push notification and do background syncs. 
    - Runs in a worker context, non-blocking, no DOM access. 