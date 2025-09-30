request: ```
```
GET / HTTP/1.1\r\n
        Request Method: GET
        Request URI: /
        Request Version: HTTP/1.1
    Host: localhost:8080\r\n
    Connection: keep-alive\r\n
    sec-ch-ua: "Chromium";v="140", "Not=A?Brand";v="24", "Google Chrome";v="140"\r\n
    sec-ch-ua-mobile: ?0\r\n
    sec-ch-ua-platform: "Windows"\r\n
    Upgrade-Insecure-Requests: 1\r\n
    User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/140.0.0.0 Safari/537.36\r\n
    Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7\r\n
    Sec-Fetch-Site: none\r\n
    Sec-Fetch-Mode: navigate\r\n
    Sec-Fetch-User: ?1\r\n
    Sec-Fetch-Dest: document\r\n
    Accept-Encoding: gzip, deflate, br, zstd\r\n
    Accept-Language: en-US,en;q=0.9\r\n
```
### What is the type of request used?
GET
### What is/are the parameter(s) of the request?
There are no parameters
### What is the version of the protocol
1.1
### What are the different headers and are they optional or mandatory in HTTP?
Host: Mandatory
Connection: Optional
sec-ch-ua: Optional
sec-ch-ua-mobile: Optional
sec-ch-ua-platform: Optional
Upgrade-Insecure-Requests: Optional
User-Agent: Optional
Accept: Optional
Sec-Fetch-Site: Optional
Sec-Fetch-User: Optional
Sec-Fetch-Dest: Optional
Accept-Encoding: Optional
Accept-Language: Optional


```
HTTP/1.1 401 Unauthorized\r\n
        Response Version: HTTP/1.1
        Status Code: 401
        [Status Code Description: Unauthorized]
        Response Phrase: Unauthorized
    Server: Tan's HTTP Server\r\n
    Date: Thu, 25 Sep 2025 08:35:11 GMT\r\n
    Cache-Control: no-cache\r\n
    Pragma: no-cache\r\n
    Expires: 0\r\n
    WWW-Authenticate: Basic realm="auth", charset="UTF-8"\r\n
    Content-Type: text/plain; charset=utf-8\r\n
    Connection: keep-alive\r\n
    Content-Length: 12\r\n

```
### What does the response code mean?
The user's request was unauthorized
### What are the different headers?
Server
Date
Pragma
Expires
WWW-Authenticate
Content-Type
Connection
Content-Length
### Is there some header that relates to the response code or authentication, what do they mean?
WWW-Authenticate is a header that is required for 401 responses. After the client receives the header, they will normally prompt the user to re-enter their credentials.
