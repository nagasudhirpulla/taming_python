## Skill - docxtpl automated reports conditional statements and loop index

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
While running this script, create folder named ```ouput``` in the same folder as the script file.

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

### Creating multiple files from single template
* In this example, we are populating  data into a template word file multiple times for each person name to create an invitation file for each person name.
```python
from docxtpl import DocxTemplate, InlineImage
import datetime as dt
from docx2pdf import convert

# template word file path
tmplPath = "inviteTmpl.docx"

personNames = ["Aakav", "Aakesh", "Aarav",
               "Advik", "Chaitanya", "Chandran", "Darsh"]

# run for each person in a for loop
for pItr, p in enumerate(personNames):
    # create a document object
    doc = DocxTemplate(tmplPath)

    # create context dictionary
    context = {
        "todayStr": dt.datetime.now().strftime("%d-%b-%Y"),
        "recipientName": p,
        "evntDtStr": "21-Oct-2021",
        "venueStr": "the beach",
        "senderName": "Sanket",
    }

    # inject image into the context
    bannerImgPath = 'images/party_banner_{0}.png'.format(pItr % 3)
    imgObj = InlineImage(doc, bannerImgPath)
    context['bannerImg'] = imgObj

    # render context into the document object
    doc.render(context)

    # save the document object as a word file
    resultFilePath = 'invites/invitation_{0}.docx'.format(pItr)
    doc.save(resultFilePath)

    # convert the word file into pdf
    convert(resultFilePath, resultFilePath.replace('.docx', '.pdf'))

print("execution complete...")
``` 

### Render a list of items using "for" loop in docxtpl templates
for loop can be used by with tables in word file templates as shown below
![docxtpl_for_loop_demo](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/docxtpl_for_loop_demo.png)
### Reports Automation example
* In this example we will create a sales report based on a word template
* An bar chart image file is created at the location ```images/trendImg.png``` using matplotlib plotting library and the image is rendered in the report using ```InlineImage``` Object

![docxtpl_reports_demo](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/docxtpl_reports_demo.png)
```python
import datetime as dt
import random
from docx2pdf import convert
import matplotlib.pyplot as plt
from docxtpl import DocxTemplate, InlineImage

# create a document object
doc = DocxTemplate("reportTmpl.docx")

# create data for reports
salesTblRows = []
for k in range(10):
    costPu = random.randint(1, 15)
    nUnits = random.randint(100, 500)
    salesTblRows.append({"sNo": k+1, "name": "Item "+str(k+1),
                         "cPu": costPu, "nUnits": nUnits, "revenue": costPu*nUnits})

topItems = [x["name"] for x in sorted(salesTblRows, key=lambda x: x["revenue"], reverse=True)][0:3]

todayStr = dt.datetime.now().strftime("%d-%b-%Y")

# create context to pass data to template
context = {
    "reportDtStr": todayStr,
    "salesTblRows": salesTblRows,
    "topItemsRows": topItems
}

# inject image into the context
fig, ax = plt.subplots()
ax.bar([x["name"] for x in salesTblRows], [x["revenue"] for x in salesTblRows])
fig.tight_layout()
fig.savefig("images/trendImg.png")
context['trendImg'] = InlineImage(doc, 'images/trendImg.png')

# render context into the document object
doc.render(context)

# save the document object as a word file
reportWordPath = 'reports/report_{0}.docx'.format(todayStr)
doc.save(reportWordPath)

# convert the word file as pdf file
convert(reportWordPath, reportWordPath.replace(".docx", ".pdf"))
```

### Video
Video for this post can be found [here](https://youtu.be/ZAVHbDB5yBQ)

<iframe width="560" height="315" src="https://www.youtube.com/embed/ZAVHbDB5yBQ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### References
* Official documentation - https://docxtpl.readthedocs.io/en/latest/

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)




<!--stackedit_data:
eyJoaXN0b3J5IjpbMTEyMzY1ODc3OCwyOTE5MzIxOTMsOTMxNT
Y3ODBdfQ==
-->