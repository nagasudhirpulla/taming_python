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
```python

``` 

### References
* Official documentation - https://docxtpl.readthedocs.io/en/latest/

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4NzA3NzE2NzgsMTgzODMyNDk1NywtOD
kzOTk2MTk2LDE4NDA4NzU2NzddfQ==
-->