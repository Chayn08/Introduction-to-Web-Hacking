# Introduction

Subdomain enumeration is the process of identifying valid subdomains for a domain. But why do we do this? The goal is to expand our attack surface and uncover more potential points of vulnerability.

In this project, we will explore three different subdomain enumeration methods: Brute Force, OSINT (Open-Source Intelligence), and Virtual Hosts.

### OSINT - SSL/TLS Certificates

When a Certificate Authority (CA) issues an SSL/TLS (Secure Sockets Layer/Transport Layer Security) certificate for a domain, it participates in what is known as Certificate Transparency (CT) logs. These logs are publicly accessible records of every SSL/TLS certificate created for a domain name. The primary purpose of CT logs is to prevent the use of malicious or mistakenly issued certificates. 

We can leverage this service to discover subdomains associated with a domain. Websites like crt.sh and Entrust CT Search provide searchable databases of certificates, offering both current and historical results.

### OSINT - Search Engines

Search engines index trillions of links across billions of websites, making them a valuable resource for finding new subdomains. By using advanced search techniques on platforms like Google, such as the site: filter, you can refine search results effectively. For example, using the query site:*.domain.com -site:www.domain.com will return results that point to subdomains of domain.com while excluding links to www.domain.com. This allows us to identify only the subdomain names associated with domain.com."

### DNS Bruteforce

Bruteforce DNS enumeration involves attempting tens, hundreds, thousands, or even millions of potential subdomains from a predefined list of commonly used subdomains. Since this method generates a high volume of requests, we automate the process using tools to increase efficiency. In this case, we utilize a tool called dnsrecon to perform the enumeration. 

### Virtual Hosts

"Hidden Subdomains and Host Header Manipulation

Some subdomains aren't always visible in publicly accessible DNS records. These could include development versions of a web application or administration portals. Such DNS records might be stored on private DNS servers or configured on developers’ machines in their /etc/hosts file (or C:\Windows\System32\drivers\etc\hosts file for Windows users), which maps domain names to IP addresses.

Since web servers can host multiple websites on a single server, they identify which site the client wants through the Host header. By modifying this header and monitoring the server’s response, we can determine if a new website is present.

Similar to DNS Bruteforce, we can automate this process using a wordlist of commonly used subdomains.
