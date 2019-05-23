# FileRun Vulnerabilities and Exploits
[FileRun](https://filerun.com) application has many vulnerabilities.

## CVE-2019-XXXX
https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-XXXX


### PoC #1 - Directory Listing
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
