## Skill - Send email with attachments in python without compromising on gmail two factor authentication

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [Reading and writing files in python](https://nagasudhir.blogspot.com/2020/05/reading-and-writing-files-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision
<hr/>

* In this post, we will learn how to send automated emails with python using smtplib python module

### Use cases
There can be many use cases for sending automated emails like sending automated reports, alerts, notifications etc.

### Python Code for sending email
* The python code below uses ```smtplib``` python library
* The following steps are implemented in this code
	* message object is created and attributes like subject, sender email, receiver email addresses, email subject, email body are set
	* attachment object is created from a local file and attached to message object
	* message object sent as email using smtplib library and mail server connection parameters

```python
import smtplib
from email.mime.text import MIMEText
from email.mime.base import MIMEBase
from email.mime.multipart import MIMEMultipart
from email import encoders
import os

def sendEmail(smtpHost, smtpPort, mailUname, mailPwd, fromEmail, mailSubject, mailContentHtml, recepientsMailList, attachmentFpaths):
    # create message object
    msg = MIMEMultipart()
    msg['From'] = fromEmail
    msg['To'] = ','.join(recepientsMailList)
    msg['Subject'] = mailSubject
    # msg.attach(MIMEText(mailContentText, 'plain'))
    msg.attach(MIMEText(mailContentHtml, 'html'))

    # create file attachments
    for aPath in attachmentFpaths:
        # check if file exists
        part = MIMEBase('application', "octet-stream")
        part.set_payload(open(aPath, "rb").read())
        encoders.encode_base64(part)
        part.add_header('Content-Disposition',
                        'attachment; filename="{0}"'.format(os.path.basename(aPath)))
        msg.attach(part)

    # Send message object as email using smptplib
    s = smtplib.SMTP(smtpHost, smtpPort)
    s.starttls()
    s.login(mailUname, mailPwd)
    msgText = msg.as_string()
    sendErrs = s.sendmail(fromEmail, recepientsMailList, msgText)
    s.quit()

    # check if errors occured and handle them accordingly
    if not len(sendErrs.keys()) == 0:
        raise Exception("Errors occurred while sending email", sendErrs)


# mail server parameters
smtpHost = "smtp.gmail.com"
smtpPort = 587
mailUname = 'senderemail@gmail.com'
mailPwd = 'ehqpsvygwbmujclq'
fromEmail = 'senderemail@gmail.com'

# mail body, recepients, attachment files
mailSubject = "test subject"
mailContentHtml = "Hi, Hope u are fine. <br/> This is a <b>test</b> mail from python script using an awesome library called <b>smtplib</b>"
recepientsMailList = ["receiveremail@gmail.com"]
attachmentFpaths = ["smtp.png", "poster.png"]
sendEmail(smtpHost, smtpPort, mailUname, mailPwd, fromEmail,
          mailSubject, mailContentHtml, recepientsMailList, attachmentFpaths)

print("execution complete...")

```
The above code can be used for Gmail or any mail server like corporate exchange server.

### App Passwords feature in Gmail
If we are using Gmail to send email from python, we can use App Passwords feature to create a separate password exclusively for the script instead of main password without sacrificing two-factor authentication and not enabling less secure apps.
#### Steps
* Login with google and visit google account page at accounts.google.com
*  Go to security tab and make sure two factor authentication is turned ON
* Click on App Passwords
* Generate an app password by selecting the app as 'Mail'
* Copy and use the generated app password instead of original gmail password in python scripts

![gmail_app_passwords_1](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/gmail_app_passwords_1.png)
![gmail_app_passwords_2](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/gmail_app_passwords_2.png)
![gmail_app_passwords_3](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/gmail_app_passwords_3.png)

### References
* Official smtplib python module documentation - https://docs.python.org/3/library/smtplib.html
* Official email python module documentation - https://docs.python.org/3/library/email.html 
* Official guide on Google app passwords - https://support.google.com/mail/answer/185833?hl=en-GB

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTI5OTA3MjQ1LC0xMjI1NzIyNzc0LC0xMD
Y2ODQwODc4LC0xMzk0MjM5ODA2LDEwNDk0NzU5NjcsLTExODkx
ODYzNjMsLTQ5MzUyNjA1NV19
-->