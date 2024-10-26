# SQL Injection

SQL Injection (SQLi) is an attack where malicious SQL commands are injected into a web application's database. It can lead to data theft, deletion, or modification and affect authentication methods. SQLi is one of the oldest and most dangerous web vulnerabilities due to its potential impact.

## SQL and Databases Basics
Databases store organized collections of data, managed by a Database Management System (DBMS), with popular types being relational (e.g., MySQL, PostgreSQL) and non-relational. Relational databases use tables to store data in rows and columns, supporting SQL for data manipulation.

Key SQL Commands:

- SELECT: Retrieves data.
- INSERT: Adds new data.
- UPDATE: Modifies existing data.
- DELETE: Removes data.
  
## Types of SQL Injection

- In-Band SQLi: Direct results returned to the attacker.
- Blind SQLi: No visible feedback, but results can still be deduced.
- Out-of-Band SQLi: Requires separate channels for data transfer, like HTTP requests sent to a controlled server.
  
## Techniques to Exploit SQL Injection

- Union-Based SQLi: Combines results from multiple tables.
- Error-Based SQLi: Uses error messages to reveal database information.
- Time-Based Blind SQLi: Uses time delays (e.g., SLEEP) to infer database responses.
- Boolean-Based Blind SQLi: Differentiates responses based on true/false conditions.
  
## SQL Injection in Practice

Attackers often test SQLi by appending syntax to manipulate the query:

- Using comments (--) to bypass part of the query.
- Using logical operators like OR 1=1 to force a true condition and gain access.
  
## Mitigation Techniques

- Prepared Statements and Parameterized Queries: Separates code from data inputs to prevent tampering.
- Input Validation: Restricts acceptable input formats and values.
- Escaping Special Characters: Adds backslashes to characters like ' " $ to prevent them from being parsed as SQL syntax.
