# Digitally sign software files with signtool.exe

## Signing software files

- Code signing is a process where software files are digitally signed with an SSL certificate
- The user can see the publisher of the software files while installing or using the software
- This helps the user to verify the authenticity and integrity of the software being installed

## How it works

- Hash of the file is calculated and encrypted with private key to create a digital signature
- This digital signature and certificate (contains public key) are bundled and appended to the file
- To verify the file, the digital signature is decrypted with the certificate and matched with the hash of the file

## Install signtool

- Download Windows SDK
- While installing just choose “Windows SDK signing Tools for Desktop Apps”

![signtool_installation.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/signtool_installation.png?raw=true)

## Sign a file with signtool.exe

- Requirements
    - pfx certificate file for code signing obtained from a Trusted Certification Authority (CA)
    - Windows SDK installation for using signtool.exe
- signtool.exe file can be found at a location like `C:\Program Files (x86)\Windows Kits\10\bin\10.0.26100.0\x64\signtool.exe`
- For example, a file `.\dist\index.exe` can be signed with signtool.exe using the following command

```powershell
"C:\Program Files (x86)\Windows Kits\10\bin\10.0.26100.0\x64\signtool.exe" sign /tr http://timestamp.digicert.com /td sha256 /fd sha256 /f certificate.pfx /p 5678 .\dist\index.exe
```

- The following command line options are used in the above command
    - `/tr` - timestamp server URL
    - `/td` - algorithm to create timestamp digest
    - `/fd` - algorithm to create file digest
    - `/f` - pfx file location
    - `/p` - pfx file password
- The signature of the `.\dist\index.exe` file can be verified using the following command

```powershell
"C:\Program Files (x86)\Windows Kits\10\bin\10.0.26100.0\x64\signtool.exe" verify /pa /v .\dist\index.exe
```

- The following command line options are used in the above command
    - `/pa` - Specifies that the Default Authentication Verification Policy is used
    - `/v` - enables verbose mode so that detailed output is printed.

## References

- Windows SDK download link - https://developer.microsoft.com/en-us/windows/downloads/windows-sdk/
- Signtool docs - https://learn.microsoft.com/en-us/windows/win32/seccrypto/signtool#examples
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwOTE3NzM1NjcsLTQ3NDUyMjAyM119
-->