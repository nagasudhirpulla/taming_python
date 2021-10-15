## Skill - python docxtpl for automating reports and invitations
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr/>

* **docxtpl** is a python library for populating data into word file templates.
* This helps in automating reports very easily. 
* Since we are using word file templates we can use rich text features like fonts, font sizes, colors etc without any programming.

The following files are used in this blog post
* Template word file - [inviteTmpl.docx](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/data/inviteTmpl.docx)
* images - [party_banner_0.png](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/party_banner_0.png), [party_banner_1.png](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/party_banner_1.png), [party_banner_2.png](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/party_banner_2.png)

While running this scripts, create two folders named ```images```, ```invites```. Download the images and move them into the images folder placed in the same folder as the script file.

### Basic Example
This is a simple example using ```docxtpl``` for populating words and images into a birthday invitation template word file. We are using the ```DocxTemplate``` and ```InlineImage``` classes in this example.
```python
from docxtpl import DocxTemplate, InlineImage
import datetime as dt

# create a document object
doc = DocxTemplate("inviteTmpl.docx")

# create context dictionary
context = {
    "todayStr": dt.datetime.now().strftime("%d-%b-%Y"),
    "recipientName": "Chaitanya",
    "evntDtStr": "21-Oct-2021",
    "venueStr": "the beach",
    "senderName": "Sanket",
}

# inject image into the context
context['bannerImg'] = InlineImage(doc, 'images/party_banner_0.png')

# render context into the document object
doc.render(context)

# save the document object as a word file
doc.save('invitation.docx')
```

### Creating multiple files from single template
* In this example, we are populating  
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
    bannerImgPath = 'images/banner{0}.png'.format(pItr % 3)
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

### References
* Official documentation - https://docxtpl.readthedocs.io/en/latest/

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwMDU0MTkwMiwxODM4MzI0OTU3LC04OT
M5OTYxOTYsMTg0MDg3NTY3N119
-->