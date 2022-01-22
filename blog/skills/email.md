## Skill - Send email with python without compromising gmail two factor authentication

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [Reading and writing files in python](https://nagasudhir.blogspot.com/2020/05/reading-and-writing-files-in-python.html)
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

msg = MIMEMultipart()
msg['From'] = mailFromEmail
msg['To'] = ','.join(recepientsMailList)
msg['Subject'] = mailSubject
# msg.attach(MIMEText(mailContentText, 'plain'))
msg.attach(MIMEText(mailContentHtml, 'html'))

# file attachment
attachmentFpath = "smtp.png"
# check if file exists - optional
part = MIMEBase('application', "octet-stream")
part.set_payload(open(attachmentFpath, "rb").read())
encoders.encode_base64(part)
part.add_header('Content-Disposition',
                'attachment; filename="{0}"'.format(os.path.basename(attachmentFpath)))
msg.attach(part)

# Send the email
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
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTc0NjAzNjMyNF19
-->