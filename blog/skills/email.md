## Skill - Send email with python without compromising gmail two factor authentication

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [Reading and writing files in python](https://nagasudhir.blogspot.com/2020/05/reading-and-writing-files-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision
<hr/>

In this post, we will learn how to send email with python using smtplib python module

### Python Code for sending email
```python
import smtplib
from email.mime.text import MIMEText
from email.mime.base import MIMEBase
from email.mime.multipart import MIMEMultipart
from email import encoders
import os

# mail server parameters
smtpHost = "smtp.gmail.com"
smtpPort = 587
mailUname = 'senderemail@gmail.com'
mailPwd = 'gcuslwchrdtqetav'
mailFromEmail = 'senderemail@gmail.com'

# mail body and recepients
mailSubject = "test subject"
mailContentHtml = "Hi, Hope u are fine. <br/> This is a <b>test</b> mail from python script using an awesome library called <b>smtplib</b>"
recepientsMailList = ["receiveremail@gmail.com"]

# create message object
msg = MIMEMultipart()
msg['From'] = mailFromEmail
msg['To'] = ','.join(recepientsMailList)
msg['Subject'] = mailSubject
# msg.attach(MIMEText(mailContentText, 'plain'))
msg.attach(MIMEText(mailContentHtml, 'html'))

# attach file to message object
attachmentFpath = "smtp.png"
# check if file exists - optional
part = MIMEBase('application', "octet-stream")
part.set_payload(open(attachmentFpath, "rb").read())
encoders.encode_base64(part)
part.add_header('Content-Disposition',
                'attachment; filename="{0}"'.format(os.path.basename(attachmentFpath)))
msg.attach(part)

# Send message object as email using smptplib
s = smtplib.SMTP(smtpHost, smtpPort)
s.starttls()
s.login(mailUname, mailPwd)
msgText = msg.as_string()
sendErrs = s.sendmail(mailFromEmail, recepientsMailList, msgText)
s.quit()

# check if errors occured and handle them accordingly
if not len(sendErrs.keys()) == 0:
    raise Exception("Errors occurred while sending email", sendErrs)

print("execution complete...")
```

### App Passwords feature in Gmail
If we are using Gmail to send email from python, we can use App Passwords feature to create a separate password exclusively for the script instead of main password without sacrificing two-factor authentication and not enabling less secure apps.

## References
* Official smtplib documentation - https://docs.python.org/3/library/smtplib.html
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTExODkxODYzNjMsLTQ5MzUyNjA1NV19
-->