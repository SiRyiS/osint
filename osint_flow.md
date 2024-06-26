# Recon

## Core Elements

| Company Information | Infrastructure            | Leaks                         |
|---------------------|---------------------------|-------------------------------|
| Organization        | Domain Information        | Archives                      |
| Locations           | Public Domain Records     | Internal Leaks                |
| Staff               | Domain Structure          | Breaches                      |
| Contact Information | Cloud Storage             | Email Addresses               |
| Business Records    |                           | Third-Parties                 |
| Services            |                           | Compounded Social Networks    |
| Social Networks     |                           | Technologies in Use           |
## Information Resources

| Information Resources |
| --------------------- |
| Home Page             |
| Files                 |
| Social Networks       |
| Search Engines        |
| Development Platforms |
| Leak Resources        |
| Forums                |
___
## Target Information
- **Organization**
	- Home Page
	- Social Networks
	- Search Engines
- **Locations**
	- Home Page
		- countries
		- cities
		- addresses
		- maps
	- Social Networks
		- LinkedIn
		- Facebook
		- Instagram
		- Twitter
		- Snapchat
		- YouTube
		- WeChat
	- Search Engines
		- Google Maps
		- Google Earth
		- Street View
		- ShowMyStreet
- **Staff**
	- Home Page
		- "about us" page
		- C-level staff bios
		- Job Listings/career page
	- Files
		- check available files metadata
			- `exiftool`
	- Social Networks
		- LinkedIn _(and others)_
			- user work details
			- Employer size
			- Job offers
				- locate specific industry target
	- Search Engines
		- search for users returned
	- Dev Platforms
		- cross with employee(s) search/job listings on Socials 
	- Leak Resources
- **Contact Info**
	- Home Page
		- "contact us" page
			- emails
			- phone
	- Social Networks
		- LinkedIn (and others)
		- mutual connections
		- contact information
	- Search Engines
		- search names
		- hunter.io for emails
			- confirm emails
				- email hippo
				- emailrep.io
		- Rocket Reach
		- whitepages
		- Dehashed
	- Leak Resources
		- WayBackMachine
- **Business Records**
	- Home Page
		- financial records
	- Files
		- search Google
			- [Google dorking](https://www.recordedfuture.com/threat-intelligence-101/threat-analysis-techniques/google-dorks)
	- Social Networks
		- search reviews
	- Search Engines
		- crunchbase
		- yahoo finance
		- 
- **Services**
	- Home Page
		- Technologies
		- possible workflows
		- employees and their respective services
		- potentially sensitive resources available
	- Files
		- relationships in files
			- "powered by" \<company\>
			- technologies used, like cloud providers 
	- Social Networks
		- leverage for further services enumeration 
	- Forums
		- treasure trove
			- Questions and answers
			- Reddit
			- StackOverflow
			- Socials 
			- wikis
			- Github
- **Social Networks**
	- Home Page
		- blogs
		- news
		- socials ^71952d
	- Social Networks
		- Look for recent and older posts, offering insights into the company's current state, structure, and technologies.
			- LinkedIn
			- Facebook
			- Instagram
			- Twitter
			- Snapchat
			- YouTube
		- Check newsletters
	- Search Engines
		- Images and videos
			- look for intel within
		- search for Docs
			- [Google dorking](https://www.recordedfuture.com/threat-intelligence-101/threat-analysis-techniques/google-dorks)
				- ex: `filetype:`
	- Forums
		- Reddit
		- StackOverflow
		- Socials
		- wikis
		- GitHub
## Infrastructure
- **Domain Info**
	- TLD, SLD information
		- Netblocks
		- Name Servers
		- Mail Servers
		- subdomains
		- hosts/IP addresses
	- Can be generally classified into 3 categories:
		- Public Records
			- ip ranges
			- DNS servers
			- Mail Servers
			- other sub-domain
				- `ffuf`
				- `sublister`
		- Third Parties
			- **Confirm scope/permissions**
			- cloud/hosting providers
			- APIs
		- Domains
			- TLD, SLD information
				- Netblocks
				- Name Servers
				- Mail Servers
				- subdomains
				- hosts/IP addresses
	- Social Networks
		- look at posts for hastags, links, etc.
		- images/videos
	- Search Engines
		- Google company name plus terms (apps, platforms, etc.)
		- Use SEO backlinks
			- [Ubersuggests](https://app.neilpatel.com/en/seo_analyzer/backlinks)
	- Dev Platforms
		- Search for company and terms
		- Look for config files, backups, etc.
			- GitHub
			- GitLab
			- Google Code
			- Bitbucket
	- Leak Resources
		- use domains/resources found to search for leaks
			- Virustotal
			- Dehashed
			- searchcode
- **Public Domain Records**
	- Need four elements:
		1. CIDR
		2. ASN
		3. DNS server(s)
		4. Mail Server(s)
	- Search Engine
		- CIDR for ip(s)
			- `host`
			- `whois`
			- `whois -h whois.arin.net <target-company> | grep -v "#" | sed -r '/^\s*$/d'
		- ASN
			- MXToolbox
			- ICANN lookup
		- DNS servers
			- `dig any <target-domain`
			- DNSdumpster
		- Mail server
			- MXToolbox
			- search found config files
	- Dev Platforms
		- search found config files
	- Leak Resources
		- use domains/resources found to search for leaks
			- Virustotal
			- Dehashed
			- searchcode
- **Domain Structure**
	- Home Page
		- pay attention to clickable area paths/re-directs
			- Passive:
				- Certificate Transparency
				- Forward DNS Datasets
				- Web Searching
				- Leaks
			- Active:
				- Subdomain brute forcing
				- AXFR
	- Search Engine
		- CTFR [ctfr.py tool](https://github.com/UnaPibaGeek/ctfr)
			- `./ctfr.py -d <target-domain> | grep -v "[-]" > subdomains.txt`
			- `for sub in $(cat subdomains.txt);do host $sub | grep "has" | cut -d" " -f1,4;done`
			- Then use `whois` and `ipcalc` to find out the IP ranges
		- IP Addresses
			- Shodan
				- **Need an account**^4be849
				- **For CLI, you need to initialize**
					- `shodan init <api_key>`
				- Web version
				- `shodan domain <TARGET-DOMAIN> | grep -w "A" | cut -d"A" -f2 | cut -d" " -f7 | sort -u > ips.txt`
				- `cat IPv4s.txt | wc -l` to get a count of unique ips
				- `for ip in $(cat ips.txt);do shodan host $ip;done`
				- check them against some resources:
					- IPinfo.io
					- VirusTotal
					- [C99.nl](https://subdomainfinder.c99.nl/index.php)
	- Dev Platforms
		- Lookout for all possible files containing hints about domain names or IPs
	- Link Resources
		- dehashed
- **Cloud**
	- Clod Providers:
		- GCP
			- Google Storage Bucket
		- AWS
			- S3 Buckets
		- Azure
			- Block Blob
		- DigitalOcean
			- Spaces
		- Use `ip2provider.py` [Tool Link](https://github.com/oldrho/ip2provider)
			- `sudo git clone https://github.com/oldrho/ip2provider.git`
			- `cd ip2provider && pip3 install -r requirements.txt`
			- Make sure you have a list of target IPs in a text file:
				- `cat <target_ips.txt> | ./ip2provider.py`
	- Home Page
		-  look for common cloud storage names
	- Search Engines
		- use Google searching
			- `inurl:`
		- GreyHatWarfare [Tool Link](https://buckets.grayhatwarfare.com/)
	- Dev Platform
		- Use Searchcode with found resources 
	- Leak Resources
		- search leak databases
		- Dehashed, etc.
- **Emails**
	- Home Page
		- Looking for general structure/format
		- "Contact us" or "About Us"
		- Career pages
	- Social Networks
		- search for conversations related to resources/target
		- Google dorking 
			- `inurl:<@domain>` & `intext:<social_platform>`
		- Email reputation on found emails
			- Emailrep.io
				- `curl -s emailrep.io/<found_email>info@<target_domain>.com`
			- Emailhippo
	- Search Engines
		- Google Dork `intext:<target_domain`
		- The Harvester
			- `python3 theHarvester.py -d inlanefreight.com -b google,hunter,netcraft,spyse,twitter,dnsdumpster`
	- Dev Platforms
		- Google Dork `inurl:<@domain>` & `inurl:github.com`
	- Leak Resources
		- Dehashed 
		- H8mail
			- `h8mail -c h8mail_config.ini -t <ex:first.lastname><@target_domain>.com`
		- HaveIBeenPwned
- **Third Parties**
	- Can be mapped to all **Information Resources**
	- Normally you should have gathered enough information to map to each along the way.
	- Tread lightly, third party resources (hosting, cloud, apps, APIs, etc.) may be OUT OF SCOPE.
	- Google Dorking

| Provider            | Dork                          |
| ------------------- | ----------------------------- |
| Google Docs         | `site:docs.google.com`        |
| Google Cloud        | `site:cloud.google.com`       |
| Google Storage      | `site:storage.googleapis.com` |
| Microsoft           | `site:docs.microsoft.com`     |
| Amazon Web Services | `site:amazonaws.com`          |

- **Compound Networks**
	- Home Page
		- Searching for socials
	- Social Networks
		- Meta (FB, IG, Threads, WhatsApp)
		- Twitter 
			- Main focus is on the content
				- Posts
				- Comments		
				- Hashtags 
				- Groups
				- Pages
				- Tags (people and content)
	- Search Engines
		- Google dork
	- Dev Platforms
		- Google dork
		- Socials searching 
	- Forums
		- Google Dork
		- Search forums themselves
- **Tech Stacks**
	- Home Page
		- source code
		- "powered by"
		- BuiltWith
	- Files
	- Social Networks
		- smart search with keywords
	- Search Engines
		- Googling
		- Shodan[[#^4be849]]
			- `shodan domain <target_domain>.com`
			- `shodan search target-company | cut -d" " -f1-3`
	- Dev Platforms
	- Forums
	- Leak Resources
## Leaks
- look out for leaks:
	- Credentials
	- Source code
	- Email Addresses
	- Tech in use
	- Third Parties
	- Domain Structure
	- Domain Info.
