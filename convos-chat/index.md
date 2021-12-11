# Cross Site Scripting - Stored through crafted SVG file in Convos-Chat before 6.32

Greeting Everyone ! Today In This Blog we will Explore XSS attack vector, Which Is Possible through SVG file Upload Functionality Due To Improper Validation Of file it got Executed to the Backend Server . 

How to Look for Stored XSS Using SVG upload

## Description
Chat component was found vulnerable to unrestricted file upload and any malicious JavaScript execution can be performed.
Stored cross-site scripting arises when an application receives data from an untrusted source and includes that data within its later HTTP responses in an unsafe way. 

## Impact
This allow an attacker to steal user session ,account takeover ,redirect user to attacker controlled site Javascript execution leads to multiple possible attack scenarios.

## Proof Of Concept
Step 1: Download the package/product from github repository https://github.com/convos-chat/convos and configure on localhost as per instruction.
Step 2: Login into the application with valid credentials.
Step 3: Navigate to chat and upload a svg file via upload functionality with below malicious JavaScript payload in it.

```<?xml version="1.0" standalone="no"?>
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">

<svg version="1.1" baseProfile="full" xmlns="http://www.w3.org/2000/svg">
   <rect width="300" height="100" style="fill:rgb(0,0,255);stroke-width:3;stroke:rgb(0,0,0)" />
   <script type="text/javascript">
      alert(document.cookie);
   </script>
</svg>
```

Step 4: Once the file is uploaded click on generated link to access the file and observe the uploaded file and JavaScript payload execution.

## Which End Point Are Vulnerable :

Profile Picture Upload
File Upload On Another Functionality
File Upload through Comment Section

## Remediation
1) Ensure that the file’s content is validated properly and input sanitization is performed.
2) Make sure a strict check against file extensions is implemented and a whitelisted is used to allow only required filetypes.
3) Make sure that the file size limit is properly validated and large files are not processed by the application.
4) Ensure that the injection points such as filename parameters are properly validated and sanitized in order to prevent client-side and     server-side injection attacks.

## Reference Links
Product url: https://github.com/convos-chat/convos
https://github.com/convos-chat/convos/issues/623
Released Fix: https://github.com/convos-chat/convos/commit/14a3b1e98cd1a3211c0ef3d4f5ffdbc60baaca54
