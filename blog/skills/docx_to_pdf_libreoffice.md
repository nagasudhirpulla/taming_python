## Automate word to PDF conversion in python using LibreOffice

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<hr/>

-   LibreOffice provides a command line interface to to convert word files to PDF
-   The conversion commands can be run in python scripts using the `subprocess` python module

## Windows

### Installation

-   Install manually from the website [](https://www.libreoffice.org/download/download-libreoffice/)[https://www.libreoffice.org/download/download-libreoffice/](https://www.libreoffice.org/download/download-libreoffice/)

### Conversion command

```powershell
"C:\\Program Files\\LibreOffice\\program\\swriter.exe" --headless --convert-to pdf --outdir "C:\\Users\\Abcd\\Documents\\liber_test\\out" "C:\\Users\\Abcd\\Documents\\liber_test\\in\\test1.docx"

```

## Ubuntu

### Installation

-   Install from command line using the following commands

```bash
# install packages
sudo apt update

# install java runtime if not present. 
# Java installation can be verified using "java -version" command
# libreoffice-java-common may be required if you get warning like "Warning: failed to launch javaldx - java may not function correctly"
sudo apt install default-jre libreoffice-java-common

# install libreoffice for word to pdf conversion purpose
sudo apt install libreoffice --no-install-recommends
```

### Conversion command

```bash
libreoffice --headless --convert-to pdf "/home/james/in/test1.docx" --outdir "/home/james/out/"

```

## Python code in windows

```python
# LibreOffice command line - https://help.libreoffice.org/latest/he/text/shared/guide/start_parameters.html

import subprocess

documentPath = r"C:\\Users\\Nagasudhir\\Documents\\Python Projects\\taming_python\\liber_pdf_convert\\in\\test1.docx"
outFolder = r"C:\\Users\\Nagasudhir\\Documents\\Python Projects\\taming_python\\liber_pdf_convert\\out"

# if running in Ubuntu, libreOfficePath = "libreoffice"
libreOfficePath = r"C:\\Program Files\\LibreOffice\\program\\swriter.exe"

commandStrings = [libreOfficePath, "--headless", "--convert-to", "pdf", "--outdir", outFolder, documentPath]
# print(" ".join(commandStrings))

retCode = subprocess.call(commandStrings)
# print(retCode)

if retCode == 0:
    print("PDF conversion completed!")
else:
    print(f"Looks like there is an error in pdf conversion process with return code {retCode}")


```

-   The output PDF file name cannot be controlled. So if required, the output file can be renamed as per requirement separately.
-   The output folder and the input file paths can also be relative paths like `.\\out` and `.\\in\\test1.docx`
-   use `soffice.com` instead of `swriter.exe` if you want to display the LibreOffice output in command line

### Python code in Ubuntu

```python
# LibreOffice command line - <https://help.libreoffice.org/latest/he/text/shared/guide/start_parameters.html>

import subprocess

documentPath = "/home/james/libre_test/in/test1.docx"
outFolder = "/home/james/libre_test/out"

# if running in Ubuntu, libreOfficePath = "libreoffice"
libreOfficePath = "libreoffice"

commandStrings = [libreOfficePath, "--headless", "--convert-to", "pdf", "--outdir", f"{outFolder}", f"{documentPath}"]
# print(" ".join(commandStrings))

retCode = subprocess.call(commandStrings)
# print(retCode)

if retCode == 0:
    print("PDF conversion completed!")
else:
    print(f"Looks like there is an error in pdf conversion process with return code {retCode}")

```

-   The output folder and the input file paths can also be relative paths like `./out` and `./in/test1.docx`


 
### Video
Video for this post can be found [here](https://youtu.be/RxBDJZhQ_D4)

<iframe width="560" height="315" src="https://www.youtube.com/embed/RxBDJZhQ_D4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### References
* Official documentation - https://github.com/AlJohri/docx2pdf
* Fix for docx2pdf pyinstaller issue - https://stackoverflow.com/a/67393186/2746323

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)




<!--stackedit_data:
eyJoaXN0b3J5IjpbNTgwNzk4NjQ1LDEzODI3OTY2OTJdfQ==
-->