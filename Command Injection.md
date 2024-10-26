# What is Command Injection?

Command injection is a vulnerability that allows an attacker to execute arbitrary commands on the host operating system via a vulnerable application. This often leads to Remote Code Execution (RCE), enabling attackers to control the application under the user’s privileges.

## Key Learning Goals

- Discover command injection vulnerabilities.
- Test and exploit these vulnerabilities on different operating systems.
- Prevent command injection in applications.
- Practice exploiting command injection in a controlled environment.
  
## How Command Injection Works

Applications may unintentionally execute OS commands through user inputs. For example, using grep or other shell commands with unsanitized input in PHP or Python allows attackers to append or inject malicious commands.

Example in PHP:

```
$command = "grep title /var/www/html/songtitle.txt";
$result = exec($command);
```

## Exploiting Command Injection

- Blind Command Injection: No direct output. Techniques like ping or sleep can be used to create a time delay and verify injection.
- Verbose Command Injection: Output is visible, such as using whoami to see the executing user.

Common Payloads for Testing:

- Linux: whoami, ls, ping, nc (netcat for reverse shells).
- Windows: whoami, dir, ping, timeout.

## Remediation

- Sanitize Inputs: Filter and validate inputs to allow only expected data types (e.g., numbers for a ping command).
- Avoid Dangerous Functions: In PHP, restrict functions like exec, passthru, and system.
- Bypass Filters: Be mindful that attackers might obfuscate payloads to bypass filters, using encoding techniques or injecting null bytes.

## Conclusion

Understanding command injection involves recognizing the vulnerability, testing it with appropriate payloads, and implementing mitigations such as input validation and filtering. This knowledge helps in preventing attackers from gaining unauthorized system control through command execution.

