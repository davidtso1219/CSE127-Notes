# Lecture 12

## Cross-Site Request Forgery (CSRF)

- an attack that forces an end user to execute unwanted actions on another web application
- typically attacking state-changing requests (POST) since the attacker can't see the result
- Example
  - user is signed into bank.com
  - bank.com sets a cookie at user's browser
  - user visits attacker.com and the malicious site sends a request to bank.com to transfer money
  - because the cookie is set, all the user's money is gone
- Defenses:
  - Validation Token
  - Referer & Origin Headers
  - Samesite Cookie Property
  - Fetch Metadata

### Validation Token

- includes a secret value in every form
- so the server can validate
- typically a session-dependent token
- attacker can't see the token because of SOP

### Referer & Origin

- Referer
  - the url of the previous web page
  - in the web page, a link to the current page is followed
- Origin
  - similar to referer
  - but only in POST requests
- Problems
  - implicitly assume GET requests have no side-effects
  - assume browsers respect cookies properties

### SameSite Cookie Property

- Cookie option that prevents browser from sending a cookie along with cross-site requests.

### Fetch Metadata

- Tell the server more about the requests
  - **Sec-Fetch-Site**: {cross-site, same-origin, same-site, none}
  - **Sec-Fetch-Mode**: {navigate, cors, no-cors, same-origin, websocker}
  - **Sec-Fetch-User**: ?1
  - **Sec-Fetch-Dest**: {audio,document,font,script,..}
- cons:
  - too new that old browsers don't support

## Command Injection

- Other examples like `eval` in JS, and `$_GET` in php

### Exmaple #1 head100

- normal input: `./head10 myfile.txt`
- bad input: `./head10 "myfile.txt; rm -rf /home"`

```c
int main(int argc, char **argv) {
  char *cmd = malloc(strlen(argv[1]) + 100)
  strcpy(cmd, “head -n 100 ”)
  strcat(cmd, argv[1])
  system(cmd);
}
```

### Example #2 Python Subprocess

```python
# incorrect
import subprocess, sys
cmd = "head -n 100 %s" % sys.arv[1]
subprocess.check_output(cmd, shell=True)

# correct (no shell, directly to the executable)
import subprocess, sys
subprocess.check_output(["head", "-n", "100", sys.argv[1]])
```

### Prevention

- Don't backlist, whitelist instead
- Use `exec` instead of shell, so only send inputs directly to the executable

## SQL Injection

- If application is blindly taking user input, then we can use `--` and quotes to build some attacks (`DROP TABLE`, run another shell command, etc.)
- Or we can use some logic trick to do something like `OR 1 = 1` to authenticate ourselves as the user

### Blind SQLi

- Result-based: use the behavior of the application to imply outcomes
- Efficient guesses via `<` and `>` (timing side-effect)
- Out-of-band channels (e.g. DNS lookup)

### Prevention

1. Parameterized SQL (Prepared SQL)
   - pass query and arguments separately to server
   - pros
     - server handles escaping automatically
     - faster because of pre-cached plan
2. Object Relational Mappers (ORM)
   - interface between native objects and relational databases

## Cross Site Scripting (XSS)

- Key idea: indirect attack on browser via server
- Malicious content is injected via URL encoding and reflected back by the server in the response
  - query parameters
  - form submission
- Browser then executes code that server provided
- Types:
  - **Reflected XSS**: The attack script is reflected back to the user as part of a page from the victim site
  - **Stored XSS**: The attacker stores the malicious code in a resource managed by the web application

### Prevention

- Filtering (cons: hard to do it right)
- Content Security Policy (CSP)

### Content Security Policy (CSP)

- Specify the valid domains to load script from (no inline script/HTML attributes)
- Two ways to specify
  - HTTP Header
  - Meta HTML Object
- Example #1:
  - content can only be loaded from same domain
  - no inline scripts
  - `Content-Security-Policy: default-src 'self'`
- Example #2:
  - Include images from any origin
  - Restrict audio or video media to trusted providers
  - Only allow scripts from a specific server that hosts trusted code
  - no inline scripts
  - `Content-Security-Policy: default-src 'self'; img-src *; media-src media1.com; script-src userscripts.example.com`

## Insecure Direct Object Reference (IDOR)

- a type of security vulnerability that occurs when an application provides improper access to objects such as files, database records, or other resources.

## Note

- Don't try to sanitize user input, never get it right.
