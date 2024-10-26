# Understanding SSRF (Server-Side Request Forgery)

1. What is SSRF?

SSRF is a vulnerability that enables attackers to manipulate a web server to make requests to unintended or restricted resources. This can be exploited to access internal systems, retrieve sensitive information, or reveal server configurations.

2. Types of SSRF

- Regular SSRF: Information from the target request is returned directly to the attacker.
- Blind SSRF: The request is made, but no data is returned to the attacker. This requires using logging tools to monitor the request’s impact.

3. Impacts of SSRF

- Unauthorized access to internal resources.
- Exposure of sensitive organizational data.
- Possibility to expand access to internal networks.
- Retrieval of authentication tokens or credentials.

## Finding SSRF Vulnerabilities
SSRF vulnerabilities can appear in various ways, such as:

- Full URLs in parameters (http://website.thm/form?server=http://server.website.thm/store)
- Hidden fields in forms with URLs (<input type="hidden" name="server" value="http://server.website.thm/store">)
- Partial URLs, like just the hostname (http://website.thm/form?server=api)
- URL paths only (http://website.thm/form?dst=/Forms/contact)

Exploiting SSRF often involves trial and error to find an accessible endpoint.

## Defense Mechanisms
1. Deny List
A deny list restricts requests to certain IP addresses or domains. For example, it might block 127.0.0.1 (localhost) to prevent internal data leakage. However, attackers may bypass deny lists using alternate forms of localhost like 2130706433 or by creating subdomains that resolve to 127.0.0.1.

2. Allow List
An allow list only permits requests to specific approved domains or IP addresses, e.g., only allowing URLs starting with https://website.thm. Attackers might circumvent this by creating a similar subdomain, such as https://website.thm.attackerdomain.com.

3. Open Redirects
In some cases, applications may have open redirects where users are redirected to external URLs. Attackers could exploit this feature to redirect SSRF requests to their own controlled domains, enabling unauthorized access or data extraction.

### Questions : 

- What website can be used to catch HTTP requests from a server?

  requestbin.com

- What method can be used to bypass strict rules?

  Open Redirect

- What IP address may contain sensitive data in a cloud environment?

  169.254.169.254

- What type of list is used to permit only certain input?

  Allow List

- What type of list is used to stop certain input?

  Deny List
  






















