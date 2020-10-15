# Project 7 - WordPress Pentesting

Time spent: **6** hours spent in total

> Objective: Find, analyze, recreate, and document **1. XSS via Media File's Metadata, 2. , 3.** affecting an old version of WordPress

## Pentesting Report

1. (Required) Vulnerability Name or ID **Authenticated Cross-Site Scripting (XSS) via Media File Metadata**
  - [x] Summary: 
    - Vulnerability types:**XSS**
    - Tested in version: **4.1**
    - Fixed in version: **4.1.16**
  - [x] GIF Walkthrough: 
  <img src="XSS_Media.gif" width="800"> 
  
  - [x] Steps to recreate:
  
    **1. Logged into word press as administrator**
    **2. Choose an image to upload and save to local machine**
    **3. Name the image file:** ```yourNameHere <img src= a onerror=alert("You're Alert Here!")>.jpg```
    **4. Navigate to 'Media' tab**
    **5. Click on 'add new'**
    **6. Browse for image/drag into the upload section**
    **7. Click on the image and select 'Edit more details'**  
    **8. Make sure the title is the name you gave the image file in step 3, with the** ```<img>``` **tag**
    **9. Then select 'View Attachment Page'**
    **10.When vieiwin the page, the alert is displayed, thus the exploit succeeds.**
  - [ ] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/tags/version/src/source_file.php)
    
    **N/A**
    
2. (Required) Vulnerability Name or ID
  - [ ] Summary: 
    - Vulnerability types:
    - Tested in version:
    - Fixed in version: 
  - [ ] GIF Walkthrough: 
  - [ ] Steps to recreate: 
  - [ ] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/tags/version/src/source_file.php)
3. (Required) Vulnerability Name or ID
  - [ ] Summary: 
    - Vulnerability types:
    - Tested in version:
    - Fixed in version: 
  - [ ] GIF Walkthrough: 
  - [ ] Steps to recreate: 
  - [ ] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/tags/version/src/source_file.php)
4. (Optional) Vulnerability Name or ID
  - [ ] Summary: 
    - Vulnerability types:
    - Tested in version:
    - Fixed in version: 
  - [ ] GIF Walkthrough: 
  - [ ] Steps to recreate: 
  - [ ] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/tags/version/src/source_file.php)
5. (Optional) Vulnerability Name or ID
  - [ ] Summary: 
    - Vulnerability types:
    - Tested in version:
    - Fixed in version: 
  - [ ] GIF Walkthrough: 
  - [ ] Steps to recreate: 
  - [ ] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/tags/version/src/source_file.php) 

## Assets

List any additional assets, such as scripts or files
**N/A**

## Resources

- [WordPress Source Browser](https://core.trac.wordpress.org/browser/)
- [WordPress Developer Reference](https://developer.wordpress.org/reference/)

GIFs created with [Kap](https://getkap.co).

## Notes

Describe any challenges encountered while doing the work

## License

    Copyright [yyyy] [name of copyright owner]

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
