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
