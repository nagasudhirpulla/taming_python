## Skill - Conditional statements, nested for loops and loop.index0 in docxtpl automated reports

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
In this blog post we will create an automated report for each customer address and each customer address will also display his other addresses and tick mark will be displayed against the address for which the report is generated   

### Template word file
The following template word file is used in this blog post can be downloaded here - [customerTmpl.docx](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/data/customerTmpl.docx)

![docxtpl_customer_template_0](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/docxtpl_customer_template_0.png)
## Code 
```python
from docxtpl import DocxTemplate
import datetime as dt
from docx2pdf import convert
import random

customerObjects = [{
    "name": "Customer 1 Name",
    "addressList": [
        ["Address 1 Flat No.", "Address 1 Street", "Address 1 City, Pin code"],
        ["Address 2 Flat No.", "Address 2 Street", "Address 2 City, Pin code"],
    ]},
    {"name": "Customer 2 Name",
     "addressList": [
         ["Address 3 Flat No.", "Address 3 Street", "Address 3 City, Pin code"],
         ["Address 4 Flat No.", "Address 4 Street", "Address 4 City, Pin code"],
     ]}
]

# template word file path
tmplPath = "customerTmpl.docx"

# run for each customer in a for loop
for cItr, cObj in enumerate(customerObjects):
    # get customer score
    cScore = random.randint(10, 90)
    # create report for each customer address in a for loop
    for addrItr in range(len(cObj["addressList"])):
        # create context dictionary
        context = {
            "todayStr": dt.datetime.now().strftime("%d-%b-%Y"),
            "recipientName": cObj['name'],
            "addressList": cObj['addressList'],
            "activeAddrInd": addrItr,
            "score": cScore
        }

        # create a document object
        doc = DocxTemplate(tmplPath)

        # render context into the document object
        doc.render(context)

        # save the document object as a word file
        resultFilePath = 'output/report_{0}_{1}.docx'.format(cItr, addrItr)
        doc.save(resultFilePath)

        # convert the word file into pdf
        pdfFilePath = resultFilePath.replace('.docx', '.pdf')
        convert(resultFilePath, pdfFilePath)

        # send the pdf file as email if required

print("execution complete...")
```
* In the above example, we have defined customers as objects and each object has customer name, customer addresses list as it's members
* In order to generate a report for each customer address, first we iterate through each customer and in turn iterate through each customer address to render a word and pdf file in the output folder
* While running this script, create folder named ```ouput``` in the same folder as the script file.
* A jinja2 `for` loop in the template word file table is used to render list of customer addresses from the context object
* We used `loop.index0` inside the jinja2 `for` loop to determine the zero-indexed loop iterator while rendering each address in the table row 
* To display check mark icon only for the report address among all the customer addresses, we have used a jinja2 `if` conditional statement that checks if the index of rendered customer address item equal to the report target address index
* 


### Video
Video for this post can be found [here](https://youtu.be/ZAVHbDB5yBQ)

<iframe width="560" height="315" src="https://www.youtube.com/embed/ZAVHbDB5yBQ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### References
* Official documentation - https://docxtpl.readthedocs.io/en/latest/

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)




<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIxMDU4NDAwNzUsLTE4MzkxMzU2NjQsMz
Y1NTg0NjkwLDI5MTkzMjE5Myw5MzE1Njc4MF19
-->