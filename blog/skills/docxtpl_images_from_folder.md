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
The template word file used in this blog post can be downloaded here - [reportTmplWithImages.docx](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/data/reportTmplWithImages.docx)

![docxtpl_images_list_template_0](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/docxtpl_images_list_template_0.png)
## Code 
* Create a folder named `images` and place the images in that folder.
* Create a folder named `reports`. The output files will be generated in that folder
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

* In the above example, we have first populated a list of python objects in a variable called `salesTblRows`. This list is used to fill the sales data table in the report template word file.
* We have used the `glob` module to iterate over all the file names in a folder location containing images and created an `InlineImage` object from each image file path.
* All the InlineImage objects are populated as in an object list variable named `imagesObjs`
* A simple context object is created with the sales table rows and images in it. This context object is rendered in the word template
* Since we are rendering a list of images, we need to use a jinja2 `for` loop inside a table to render the list of images in the word file template.
* To make the table look like a list, we have removed the borders of the table in the word file.
* If the images are wider than the word file page width (A4 size page width is 8.3 inches), they will rendered as cropped images, which is not desirable. To mitigate this, we have specified the `width=Inches(6)` input to the `InlineImage` constructor to resize the image to have a width of 6 inches.
* If you specify the image width more than that of the original image, it can result in images rendering with bad pixel density. So make sure images that are rendered have minimum width as per our requirements

### Output
As shown in the below image, a word and pdf file is generated for each customer address and check mark is set for the report address
![docxtpl_images_list_output_0](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/docxtpl_images_list_output_0.png)
### Video
Video for this post can be found [here](https://youtu.be/mcZkZvkwgFA)

<iframe width="560" height="315" src="https://www.youtube.com/embed/mcZkZvkwgFA" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### References
* Official documentation - https://docxtpl.readthedocs.io/en/latest/
* Previous blog post - https://nagasudhir.blogspot.com/2021/10/docxtpl-python-library-for-creating.html

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)




<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2NTQ4MTk1MzcsMjA0MDkyOTIxMiw2Nj
I3NDc0MDYsLTE3MzM4MDM5MDMsLTE3MTA1MTU4OTYsLTE1OTAy
ODk5ODEsLTE0NjIwODIyMTNdfQ==
-->