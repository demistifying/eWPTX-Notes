### OWASP ZAP Context and Scope
- Right click site in scope > Include in context > Default context
- Click 'Show only URLs in scope' (Bullseye icon)

### Website Screenshots with EyeWitness

```bash
  sudo apt-get install eyewitness
  
  eyewitness --web -f domains.txt -d folder
```

- Web application fingerprinting
- Pair with `httrack`

### Website Recon and Footprinting
- Information to look for:
	- IP Address
	- Directories hidden from search engines
	- Names, email address, phone numbers
	- Physical addresses
	- Web technologies used

- ```bash
  host example.org
   ```

- example.com/robots.txt - list of endpoints/directories disallowed for search engines
- example.com/sitemap.xml - lists all directories for search engines to crawl
- identify tech stack of the website
	- Wappalyzer 
	- builtwith extension/add-on 
	- ```bash
	  whatweb example.com
	  ```
- `httrack` - website copier

### Email harvesting
- Gather names, emails, IPs, subdomains, URLS using theHarvester
- ```bash
  theHarvester -d example.com -b duckduckgo,baidu,bing,yahoo,hunter,brave,urlscan
  ```

### Leaked Password Databases 
- https://haveibeenpwned.com - check if email or password was leaked in data breach

### Google Dorking
- `site:example.com inurl:admin` 
- `site:*.ine.com` (subdomain enumeration)
- `site:*.ine.com intitle:admin`
- `site:*.ine.com filetype:pdf`
- `intitle:index of`
- `cache:example.com` (Alternative: Wayback Machine)
- `inurl:auth_user_file.txt`
- `intitle:passwd.txt`
- `inurl:wp-config.bak`
- [Google hacking database](https://www.exploit-db.com/google-hacking-database) - Cheat sheet resource

### HTTrack - Copying websites for analysis
- https://www.httrack.com

```bash
mkdir directory
httrack example.com -O directory/
```