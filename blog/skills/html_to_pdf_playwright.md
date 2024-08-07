# HTML to PDF conversion in python with playwright

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

-   We can convert a HTML to PDF by printing it in a browser window
-   playwright is a python module for browser automation that can be used to automate the task of printing a HTML page to pdf in browser
-   The required browser (like chromium, Firefox etc.) for automation can also be installed using playwright

## Install playwright python module

-   `python -m pip install pytest-playwright`

## Install browsers for playwright

-   For printing pdf, we are using chromium. Run the following command to install chromium browser for playwright
-   `python -m playwright install chromium`
-   For installing other browsers, run the following command to know the possible options
-   `python -m playwright install --help`

## Example python script

-   The following script converts a local HTML file into a pdf file using python playwright module

```python
from playwright.sync_api import sync_playwright
import pathlib
import os

# convert a relative path of a local file into absolute path
# you can skip this if you have an absolute path like "C:\\Users\\James\\reports\\sales_report.html"
filePath = os.path.abspath("reports/sales_report.html")

# derive the URL path of a local file to be opened in browser
fileUrl = pathlib.Path(filePath).as_uri()

# print the file as a pdf from chromium browser using playwright
with sync_playwright() as p:
    # create a browser instance
    browser = p.chromium.launch()

    # open a new tab in the browser
    page = browser.new_page()

    # goto the URL of the HTML page
    page.goto(fileUrl)

    # change css media type to screen
    page.emulate_media(media="screen")

    # print the html page as pdf in the browser
    page.pdf(path="reports/sales_report.pdf", format="A4",
             landscape=True, margin={"top": "2cm"})
    
    # close the browser
    browser.close()

```

The above script does the following

-   Derive the URL of the HTML file to be printed
-   Open the HTML file in a playwright browser tab using the URL
-   Print the HTML page as a PDF and save it in the desired location

### Video
Video on this post can be seen [here](https://youtu.be/_L6ELUJN-9Q?si=Zel1XwhS9qACl90I)

<iframe width="560" height="315" src="https://www.youtube.com/embed/_L6ELUJN-9Q?si=nfdzNgUb5dhPZHRn" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

## References

-   Playwright docs - [https://playwright.dev/python/docs/intro](https://playwright.dev/python/docs/intro)
-   Playwright `pdf` function - [https://playwright.dev/python/docs/api/class-page#page-pdf](https://playwright.dev/python/docs/api/class-page#page-pdf)
<!--stackedit_data:
eyJoaXN0b3J5IjpbNjI5Nzg1MjU2LC0xODEyNDQwMzY2LDEyMD
kyNzIwNTAsLTk0NDc5NDgwMV19
-->