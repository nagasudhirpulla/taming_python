## Skill - Render images from folder in automated reports using python docxtpl

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [docxtpl python library for creating automated reports as word and pdf files from templates](https://nagasudhir.blogspot.com/2021/10/docxtpl-python-library-for-creating.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr/>

* **docxtpl** is a python library for populating data into word file templates.
* Please see the previous blog post [here](https://nagasudhir.blogspot.com/2021/10/docxtpl-python-library-for-creating.html) for introduction and in-depth use cases of docxtpl for report automation

## Problem description
In this blog post we will render all the images present in a folder in a word file template using python docxtpl

### Template word file
The following template word file is used in this blog post can be downloaded here - [reportTmplWithImages.docx](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/data/reportTmplWithImages.docx)

![docxtpl_images_list_template_0](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/docxtpl_images_list_template_0.png)
## Code 
```python
import datetime as dt
import random
from docx2pdf import convert
import glob
from docxtpl import DocxTemplate, InlineImage
from docx.shared import Inches

# create a document object
doc = DocxTemplate("reportTmplWithImages.docx")

# populate sales table rows with each row data as a python object
salesTblRows = []
for k in range(10):
    costPu = random.randint(1, 15)
    nUnits = random.randint(100, 500)
    salesTblRows.append({"name": "Item "+str(k+1),
                         "cPu": costPu, "nUnits": nUnits, "revenue": costPu*nUnits})

# get today's date as a string
todayStr = dt.datetime.now().strftime("%d-%b-%Y")

# populate list of images with each list item as a docxtpl image object
imagesObjs = []
for fPath in glob.glob("images/*"):
    imagesObjs.append(InlineImage(doc, fPath, width=Inches(6)))

# create context to pass data to template
context = {
    "reportDtStr": todayStr,
    "salesTblRows": salesTblRows,
    "images": imagesObjs
}

# render context into the document object
doc.render(context)

# save the document object as a word file
reportWordPath = 'reports/report_{0}.docx'.format(todayStr)
doc.save(reportWordPath)

# convert the word file as pdf file
convert(reportWordPath, reportWordPath.replace(".docx", ".pdf"))
```
* In the above example, we have defined customers as objects and each object has customer name, customer addresses list as it's members
* In order to generate a report for each customer address, first we iterate through each customer and in turn iterate through each customer address to render a word and pdf file in the output folder
* While running this script, create folder named ```ouput``` in the same folder as the script file.
* A jinja2 `for` loop in the template word file table is used to render list of customer addresses from the context object
* We used `loop.index0` inside the jinja2 `for` loop to determine the zero-indexed loop iterator while rendering each address in the table row 
* To display check mark icon only for the target report address among all the customer addresses, we have used a jinja2 `if` conditional statement that checks if the index of the rendered customer address is equal to the target address index
* Each line of the address is rendered as a word table row using jinja2 `for` loop. Hence we are using a for loop inside a for loop.

### Output
As shown in the below image, a word and pdf file is generated for each customer address and check mark is set for the report address
![docxtpl_example_output_0](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/docxtpl_example_output_0.png)
### Video
Video for this post can be found [here](https://youtu.be/KV6iHKhJDdM)

<iframe width="560" height="315" src="https://www.youtube.com/embed/KV6iHKhJDdM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### References
* Official documentation - https://docxtpl.readthedocs.io/en/latest/
* Previous blog post - https://nagasudhir.blogspot.com/2021/10/docxtpl-python-library-for-creating.html

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)




<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzODU2OTY2ODgsLTE0NjIwODIyMTNdfQ
==
-->