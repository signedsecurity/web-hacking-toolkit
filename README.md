<h1 align="center">Web Hacking ToolKit</h1>

<p align="center">
	<a href="https://github.com/signedsecurity/web-hacking-toolkit/actions">
		<img alt="GitHub Workflow Status" src="https://img.shields.io/github/workflow/status/signedsecurity/web-hacking-toolkit/🎉%20CI%20to%20Docker%20Hub">
	</a>
	<a href="https://github.com/signedsecurity/web-hacking-toolkit/issues?q=is:issue+is:open">
		<img alt="GitHub Open Issues" src="https://img.shields.io/github/issues-raw/signedsecurity/web-hacking-toolkit.svg">
	</a>
	<a href="https://github.com/signedsecurity/web-hacking-toolkit/issues?q=is:issue+is:closed">
		<img alt="GitHub Closed Issues" src="https://img.shields.io/github/issues-closed-raw/signedsecurity/web-hacking-toolkit.svg">
	</a>
	<a href="https://github.com/signedsecurity/web-hacking-toolkit/graphs/contributors">
		<img alt="GitHub contributors" src="https://img.shields.io/github/contributors/signedsecurity/web-hacking-toolkit">
	</a>
	<a href="https://github.com/signedsecurity/web-hacking-toolkit/blob/master/LICENSE">
		<img alt="GitHub" src="https://img.shields.io/github/license/signedsecurity/web-hacking-toolkit">
	</a>
</p>

<p align="center">
	<a href="https://hub.docker.com/r/signedsecurity/web-hacking-toolkit/">
		<img alt="Docker Automated build" src="https://img.shields.io/docker/automated/signedsecurity/web-hacking-toolkit">
	</a>
	<a href="https://hub.docker.com/r/signedsecurity/web-hacking-toolkit/">
		<img alt="Docker Pulls" src="https://img.shields.io/docker/pulls/signedsecurity/web-hacking-toolkit">
	</a>
	<a href="https://hub.docker.com/r/signedsecurity/web-hacking-toolkit/">
		<img alt="Docker Starts" src="https://img.shields.io/docker/stars/signedsecurity/web-hacking-toolkit">
	</a>
	<a href="https://hub.docker.com/r/signedsecurity/web-hacking-toolkit/">
		<img alt="Docker Image Size" src="https://img.shields.io/docker/image-size/signedsecurity/web-hacking-toolkit/latest">
	</a>
</p>

A web hacking toolkit docker image with GUI applications support.

## Resources

* [Installation](#installation)
    * [Docker](#docker)
    * [Docker Compose](#docker-compose)
    * [Build from Source](#build-from-source)
* [GUI Support](#gui-support)
    * [Using SSH with X11 forwarding](#using-ssh-with-x11-forwarding)
* [Installed](#installed)
    * [Tools](#tools)
    * [Wordlists](#wordlists)

## Installation

### Docker

Pull the image from Docker Hub:

```bash
docker pull signedsecurity/web-hacking-toolkit
```

Run a container and attach a shell:

```bash
docker run \
	-it \
	--rm \
	--shm-size="2g" \
	--name web-hacking-toolkit \
	--hostname web-hacking-toolkit \
	-p 22:22 \
	-v $(pwd)/data:/root/data \
	signedsecurity/web-hacking-toolkit \
	/bin/bash
```
### Docker Compose

Docker-Compose can also be used.

```yaml
version: "3.9"

services:
    web-hacking-toolkit:
        image: signedsecurity/web-hacking-toolkit
        container_name: web-hacking-toolkit
        hostname: web-hacking-toolkit
        stdin_open: true
        shm_size: 2gb # increase shared memory size to prevent firefox from crashing
        ports:
            - "22:22" # exposed for GUI support sing SSH with X11 forwarding
        volumes:
            - ./data:/root/data
        restart: unless-stopped
```

Build and run container:

```bash
docker-compose up
```

Attach shell:

```bash
docker-compose exec web-hacking-toolkit /bin/bash
```

### Build from Source

Clone this repository and build the image:

```bash
git clone https://github.com/signedsecurity/web-hacking-toolkit.git && \
cd web-hacking-toolkit && \
make build-image
```

Run a container and attach a shell:

```bash
make run
```

## GUI Support

By default, no GUI tools can be run in a Docker container as no X11 server is available. To run them, you must change that. What is required to do so depends on your host machine. If you:

* run on Linux, you probably have X11
* run on Mac OS, you need Xquartz (`brew install Xquartz`)
* run on Windows, you have a problem

### Using SSH with X11 forwarding

Use X11 forwarding through SSH if you want to go this way. Run `start_ssh` inside the container to start the server, make sure you expose port 22 when starting the container: `docker run -p 127.0.0.1:22:22 ...`, then use `ssh -X ...` when connecting (the script prints the password).

## Installed

### Tools

| Name | Description |
| :--- | :---------- |
| [Amass](https://github.com/OWASP/Amass) | In-depth Attack Surface Mapping and Asset Discovery |
| [anew](https://github.com/tomnomnom/anew) | A tool for adding new lines to files, skipping duplicates |
| [Arjun](https://github.com/s0md3v/Arjun) | HTTP parameter discovery suite. |
| [Burp Suite Community](https://portswigger.net/burp) | The BurpSuite Project  community edition. |
| [cdncheck](https://github.com/enenumxela/cdncheck) | A CLI wrapper for ProjectDiscovery's cdncheck library - "Helper library that checks if a given IP belongs to known CDN ranges (akamai, cloudflare, incapsula and sucuri)". |
| [cent](https://github.com/xm1k3/cent) | Community edition nuclei templates, a simple tool that allows you to organize all the Nuclei templates offered by the community in one place. |
| [chrome](https://www.google.com/chrome/) | Chrome is a fast, secure, free web browser built by Google. |
| [commix](https://github.com/commixproject/commix) | Automated All-in-One OS Command Injection Exploitation Tool. |
| [crlfuzz](https://github.com/dwisiswant0/crlfuzz) | A fast tool to scan CRLF vulnerability written in Go |
| [curl](https://github.com/curl/curl) | A command line tool and library for transferring data with URL syntax, supporting HTTP, HTTPS, FTP, FTPS, GOPHER, TFTP, SCP, SFTP, SMB, TELNET, DICT, LDAP, LDAPS, MQTT, FILE, IMAP, SMTP, POP3, RTSP and RTMP. libcurl offers a myriad of powerful features |
| [dalfox](https://github.com/hahwul/dalfox) | waning_crescent_moonfox_face DalFox(Finder Of XSS) / Parameter Analysis and XSS Scanning tool based on golang |
| [dnsvalidator](https://github.com/vortexau/dnsvalidator) | Maintains a list of IPv4 DNS servers by verifying them against baseline servers, and ensuring accurate responses. |
| [dnsx](https://github.com/projectdiscovery/dnsx) | dnsx is a fast and multi-purpose DNS toolkit allow to run multiple DNS queries of your choice with a list of user-supplied resolvers. |
| [dotdotpwn](https://github.com/wireghoul/dotdotpwn) | DotDotPwn - The Directory Traversal Fuzzer |
| [ffuf](https://github.com/ffuf/ffuf) | Fast web fuzzer written in Go |
| [findomain](https://github.com/Edu4rdSHL/findomain) | The fastest 
| [firefox](https://www.mozilla.org/en-US/firefox/new/) | Safe and easy web browser from Mozilla |and cross-platform subdomain enumerator, do not waste your time. |
| [gowitness](https://github.com/sensepost/gowitness) | mag gowitness - a golang, web screenshot utility using Chrome Headless |
| [hakrevdns](https://github.com/hakluke/hakrevdns) | Small, fast, simple tool for performing reverse DNS lookups en masse. |
| [httpx](https://github.com/projectdiscovery/httpx) | httpx is a fast and multi-purpose HTTP toolkit allow to run multiple probers using retryablehttp library, it is designed to maintain the result reliability with increased threads. |
| [kiterunner](https://github.com/assetnote/kiterunner) | Contextual Content Discovery Tool |
| [masscan](https://github.com/robertdavidgraham/masscan) | TCP port scanner, spews SYN packets asynchronously, scanning entire Internet in under 5 minutes. |
| [massdns](https://github.com/blechschmidt/massdns) | A high-performance DNS stub resolver. |
| [naabu](https://github.com/projectdiscovery/naabu) | A fast port scanner written in go with focus on reliability and simplicity. Designed to be used in combination with other tools for attack surface discovery in bug bounties and pentests |
| [nmap](https://github.com/nmap/nmap) | Nmap - the Network Mapper. Github mirror of official SVN repository. |
| [nuclei](https://github.com/projectdiscovery/nuclei) | Nuclei is a fast tool for configurable targeted scanning based on templates offering massive extensibility and ease of use. |
| [ping](https://github.com/iputils/iputils) | Tools to test the reachability of network hosts. |
| [ps.sh](https://github.com/enenumxela/ps.sh) | A wrapper around tools used for port scanning(nmap, naabu & masscan), the goal being reducing scan time, increasing scan efficiency and automating the workflow. |
| [puredns](https://github.com/d3mondev/puredns) | Puredns is a fast domain resolver and subdomain bruteforcing tool that can accurately filter out wildcard subdomains and DNS poisoned entries.  |
| [sigsubfind3r](https://github.com/signedsecurity/sigsubfind3r) | A subdomain discovery tool - it gathers a list of subdomains passively using various online sources. |
| [sigurlfind3r](https://github.com/signedsecurity/sigurlfind3r) | A passive reconnaissance tool for known URLs discovery - it gathers a list of URLs passively using various online sources. |
| [sigurlscann3r](https://github.com/signedsecurity/sigurlscann3r) | A web application attack surface mapping tool. It takes in a list of urls then performs numerous probes |
| [sqlmap](https://github.com/sqlmapproject/sqlmap) | Automatic SQL injection and database takeover tool |
| [subdomains.sh](https://github.com/enenumxela/subdomains.sh) | A wrapper around for subdomains gathering tools (amass, subfinder, findomain & sigsubfind3r) to increase gathering efficiency and automating the workflow. |
| [subfinder](https://github.com/projectdiscovery/subfinder) | Subfinder is a subdomain discovery tool that discovers valid subdomains for websites. Designed as a passive framework to be useful for bug bounties and safe for penetration testing. |
| [urlx](https://github.com/enenumxela/urlx) | A go(golang) utility for URLs parsing & pull out bits of the URLS. |
| [waf00f](https://github.com/EnableSecurity/wafw00f) | The Web Application Firewall Fingerprinting Tool. |
| [wappalyzer](https://github.com/aliasio/wappalyzer) | Wappalyzer identifies technologies on websites, such as CMS, web frameworks, ecommerce platforms, JavaScript libraries, analytics tools and more. |
| whois | whois - client for the whois directory service |
| [whatweb](https://github.com/urbanadventurer/WhatWeb) | Next generation web scanner. |
| [wprecon](https://github.com/blackcrw/wprecon) | WPRecon, is a tool for the recognition of vulnerabilities and blackbox information for wordpress. |
| [wpscan](https://github.com/wpscanteam/wpscan) | WordPress Security Scanner |
| [wuzz](https://github.com/asciimoo/wuzz) | Interactive cli tool for HTTP inspection |

### Wordlists

| Wordlist | Description |
| :------- | :---------- |
| [Assetnote](https://wordlists.assetnote.io/) | Assetnote provides you with wordlists that are up to date and effective against the most popular technologies on the internet. Wordlists are generated on the 28th of each month, using Commonspeak2 and GitHub Actions. |
| [blechschmidt's massdns resolvers.txt](https://github.com/blechschmidt/massdns/blob/master/lists/resolvers.txt) | DNS Resolvers |
| [leaky-paths](https://github.com/ayoubfathi/leaky-paths) | A collection of special paths linked to major web CVEs, known juicy APIs, misconfigurations.. etc. |
| [SecLists](https://github.com/danielmiessler/SecLists) | SecLists is the security tester's companion. It's a collection of multiple types of lists used during security assessments, collected in one place. List types include usernames, passwords, URLs, sensitive data patterns, fuzzing payloads, web shells, and many more. |
| [six2dev's permutations_list.txt](https://gist.github.com/six2dez/ffc2b14d283e8f8eff6ac83e20a3c4b4) | Permutations Wordlist |