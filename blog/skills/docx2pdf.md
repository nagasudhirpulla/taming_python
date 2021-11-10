## Skill - Automating word files to pdf files conversion using docx2pdf python library

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr/>

* **docx2pdf** is a python library for converting word file to pdf file
* This helps in automating word files to pdf files in bulk and without manual intervention 
* docx2pdf can be used as a command line tool and also in python program

### Install docx2pdf python module
* Open command prompt
* Run the command ```python -m pip install docx2pdf```
* Now docx2pdf should be installed in your python environment

### Prerequisites
docx2pdf requires Microsoft Word to be installed in the computer

### Python example
```python
import docx2pdf
# convert "abcd.docx" file to pdf in the same folder
docx2pdf.convert("abcd.docx")

# convert "abcd.docx" file to pdf with custom name and folder location
docx2pdf.convert("abcd.docx", "out/abc.pdf")

# convert all the docx files in a folder. 
# Output files will also be in the same folder
docx2pdf.convert("inp/")

# convert all the docx files in a folder and keep the pdfs in another folder
docx2pdf.convert("inp/", "out/")
```

### Command line interface
* Convert a single word file to pdf
```batch
docx2pdf file1.docx
```
The above command converts file1.docx to file1.pdf 
* convert all word files in a folder to pdf files
```batch
docx2pdf folder1/
```
The above command converts all the word files in folder1 to pdf files
* Convert single docx file and output to a different explicit folder:
```batch
docx2pdf inputFile.docx outputFolder/
```
* Batch convert docx folder. Output PDFs will go to a different explicit folder:
```batch
docx2pdf inpFoldr/ outDir/
```

### Issues while packaging the code to exe with pyinstaller
You might get errors like ```#[ImportError with cx_freeze and pywin32: Module 'pythoncom' isn't in frozen sys.path](https://stackoverflow.com/questions/17891071/importerror-with-cx-freeze-and-pywin32-module-pythoncom-isnt-in-frozen-sys-p)```

### Video
Video for this post can be found [here](https://youtu.be/RxBDJZhQ_D4)

<iframe width="560" height="315" src="https://www.youtube.com/embed/RxBDJZhQ_D4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### References
* Official documentation - https://github.com/AlJohri/docx2pdf
* Fix for docx2pdf pyinstaller issue - https://stackoverflow.com/a/67393186/2746323

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)




<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1MTg1ODExNTUsMTc0MzIwNjg5OSwtMT
E0ODU1MzU1LC0xMTk4ODQ2NTE0LC0xNjc2MzY2MTgzLC0xMDQy
MzcxNTg1XX0=
-->