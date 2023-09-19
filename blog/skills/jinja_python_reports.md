## Automated reports with rich styling and interactivity using python and jinja2 HTML templates

## Jinja templates

-   Jinja template is a text file with named placeholders
-   The named placeholders in Jinja templates can be substituted with desired text using python
-   A HTML file with jinja placeholders can be used as report template to generate reports
-   Since the generated report is a HTML document, the reports can be generated like web pages with rich styling and interactivity

## Installing jinja2

-   Run the following command to install jinja2 with pip

```powershell
python -m pip install jinja2

```

## jinja template rendering simple example

-   In this example we will substitute data in a string using jinja templating
-   The named variables are declared in the template using double curly braces (like `{{senderName}}`)
-   The jinja template can be loaded from a string variable or from a file

```python
import jinja2
import datetime as dt

# jinja template
templateStr = """Hi {{recipientName}},
Your presence at the birthday party will bring great delight in our hearts. We are looking forward to hosting you at the birthday party of our child on {{evntDtStr}} at {{venueStr}}

Join us at the birthday party and make the night magical while showering us with your blessing.

Regards
{{senderName}}
"""

# create jinja template object from a string
template = jinja2.Environment(
    loader=jinja2.BaseLoader
).from_string(templateStr)

"""
# create jinja template object from file
template = jinja2.Environment(
    loader=jinja2.FileSystemLoader("./templates")
).get_template("invite_template.txt")
"""

# data for injecting into jinja2 template
templateContext = {
    "todayStr": dt.datetime.now().strftime("%d-%b-%Y"),
    "recipientName": "",
    "evntDtStr": "21-Oct-2021",
    "venueStr": "the beach",
    "senderName": "Sanket",
}

guests = ["Aakav", "Aakesh", "Aarav",
          "Advik", "Chaitanya", "Chandran", "Darsh"]

for g in guests:
    templateContext["recipientName"] = g

    # render data in jinja template
    inviteText = template.render(templateContext)

    # print(inviteText)
    with open(f"./invites/{g}.txt", mode='w') as f:
        f.write(inviteText)

```

## HTML jinja templates example

-   Jinja variable placeholders, conditional statements, for loops can be used in a HTML file and can be used as a template
-   Variable placeholders can be kept in HTML attributes, CSS, JavaScript to control the styling and interactivity of the generated HTML files
-   The following example generates a sales report from a HTML template

### Python script

```python
# index.py file
import base64
import datetime as dt
import io
import random
import jinja2
import matplotlib.pyplot as plt

# Step 1 - create data for report
salesTblRows = []
for k in range(10):
    costPu = random.randint(1, 15)
    nUnits = random.randint(100, 500)
    salesTblRows.append({"sNo": k+1, "name": "Item "+str(k+1),
                         "cPu": costPu, "nUnits": nUnits, "revenue": costPu*nUnits})

topItems = [x["name"] for x in sorted(
    salesTblRows, key=lambda x: x["revenue"], reverse=True)][0:3]

todayStr = dt.datetime.now().strftime("%d-%b-%Y")

# create logo image from file
with open("templates/logo.png", "rb") as f:
    logoImg = base64.b64encode(f.read()).decode()

# generate sales bar chart image
plotImgBytes = io.BytesIO()
fig, ax = plt.subplots()
ax.bar([x["name"] for x in salesTblRows], [x["revenue"] for x in salesTblRows])
fig.tight_layout()
fig.savefig(plotImgBytes, format="jpg")
plotImgBytes.seek(0)
plotImgStr = base64.b64encode(plotImgBytes.read()).decode()

# data for injecting into jinja2 template
context = {
    "reportDtStr": todayStr,
    "salesTblRows": salesTblRows,
    "topItemsRows": topItems,
    "salesBarChartImg": plotImgStr,
    "logoImg": logoImg,
}

# Step 2 - create jinja template object from file
template = jinja2.Environment(
    loader=jinja2.FileSystemLoader("./templates"),
    autoescape=jinja2.select_autoescape
).get_template("sales_report_template.html")

# Step 3 - render data in jinja template
reportText = template.render(context)

# Step 4 - Save genereate text as a HTML file
reportPath = "./reports/sales_report.html"
with open(reportPath, mode='w') as f:
    f.write(reportText)

```

-   A jinja for loop is also used to render list of items as HTML table rows and HTML list items
-   A logo image from an image file is converted as base64 encoded string for rendering as a HTML image. The bar chart image bytes generated with matplotlib is also rendered as base64 encoded string for rendering as a HTML image
-   The autoescape option in jinja template environment is set to `jinja2.select_autoescape` which prevents injecting HTML into the jinja variable placeholders. This can be used as a security measure to prevent HTML injection in the jinja templates

### HTML Template

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Report for {{reportDtStr}}</title>
    <style>
        body {
            margin: 2em;
            font-family: Arial, Helvetica, sans-serif;
        }

        table,
        th,
        td {
            border: 1px solid #555;
            border-collapse: collapse;
            padding: 0.25em;
        }
    </style>
</head>

<body class="container">
    <img class="img-fluid" src="data:image/png;base64, {{logoImg}}" alt="logo"
        style="float: left; width:50px; height:50px; margin-right: 0.5em;">
    <div>
        <span>Daily sales report for {{reportDtStr}}</span><br>
        <span>Acme Inc.</span>
    </div>
    <hr>
    <div style="margin-top: 2em;"></div>
    <table class="table">
        <thead>
            <tr>
                <th>S.No</th>
                <th>Item Name</th>
                <th>Cost per Unit</th>
                <th>Units Sold</th>
                <th>Revenue </th>
            </tr>
        </thead>
        <tbody>
            {% for item in salesTblRows %}
            <tr>
                <td>{{item.sNo}}</td>
                <td>{{item.name}}</td>
                <td>{{item.cPu}}</td>
                <td>{{item.nUnits}}</td>
                <td>{{item.revenue}}</td>
            </tr>
            {% endfor %}
        </tbody>
    </table>

    <h2>Top performing items</h2>
    <ul class="list-group">
        {% for item in topItemsRows %}
        <li class="list-group-item">{{item}}</li>
        {% endfor %}
    </ul>
    <p style="page-break-after: always;">&nbsp;</p>
    <h2>Revenue Bar Chart</h2>
    <img class="img-fluid" src="data:image/jpeg;base64, {{salesBarChartImg}}" alt="Revenue Bar Chart Image">
</body>

</html>

```

### Output

![https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/jinja_html_report_demo.png?raw=true](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/jinja_html_report_demo.png?raw=true)

## HTML Jinja templates with external CSS and JavaScript

### HTML Template

```html
<!-- templates/sales_report_template_bootstrap.html -->
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Report for {{reportDtStr}}</title>
    <link href="<https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css>" rel="stylesheet">
    <!-- <style>
        {{bootstrapCss}}
    </style> -->
    <style>
        body {
            margin: 2em;
        }
    </style>
</head>

<body class="container">
    <img class="img-fluid" src="data:image/png;base64, {{logoImg}}" alt="logo"
        style="float: left; width:50px; height:50px; margin-right: 0.5em;">
    <div>
        <span>Daily sales report for {{reportDtStr}}</span><br>
        <span>Acme Inc.</span>
    </div>
    <hr>

    <div style="margin-top: 2em;"></div>
    
    <table class="table table-striped table-bordered">
        <thead>
            <tr>
                <th>S.No</th>
                <th>Item Name</th>
                <th>Cost per Unit</th>
                <th>Units Sold</th>
                <th>Revenue </th>
            </tr>
        </thead>
        <tbody>
            {% for item in salesTblRows %}
            <tr>
                <td>{{item.sNo}}</td>
                <td>{{item.name}}</td>
                <td>{{item.cPu}}</td>
                <td>{{item.nUnits}}</td>
                <td>{{item.revenue}}</td>
            </tr>
            {% endfor %}
        </tbody>
    </table>

    <h2>Top performing items</h2>
    <ul class="list-group">
        {% for item in topItemsRows %}
        <li class="list-group-item">{{item}}</li>
        {% endfor %}
    </ul>
    <p style="page-break-after: always;">&nbsp;</p>
    <h2>Revenue Bar Chart</h2>
    <img class="img-fluid" src="data:image/jpeg;base64, {{salesBarChartImg}}" alt="Revenue Bar Chart Image">
    <script src="<https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js>"></script>
    <!-- <script type="text/application">
        {{bootstrapJs}}
    </script> -->
</body>

</html>

```

### Python script

```python
import base64
import datetime as dt
import io
import random
import jinja2
import matplotlib.pyplot as plt
import pdfkit

# Step 1 - create data for report
salesTblRows = []
for k in range(10):
    costPu = random.randint(1, 15)
    nUnits = random.randint(100, 500)
    salesTblRows.append({"sNo": k+1, "name": "Item "+str(k+1),
                         "cPu": costPu, "nUnits": nUnits, "revenue": costPu*nUnits})

topItems = [x["name"] for x in sorted(
    salesTblRows, key=lambda x: x["revenue"], reverse=True)][0:3]

todayStr = dt.datetime.now().strftime("%d-%b-%Y")

# create logo image from file
with open("templates/logo.png", "rb") as f:
    logoImg = base64.b64encode(f.read()).decode()

# generate sales bar chart image
plotImgBytes = io.BytesIO()
fig, ax = plt.subplots()
ax.bar([x["name"] for x in salesTblRows], [x["revenue"] for x in salesTblRows])
fig.tight_layout()
fig.savefig(plotImgBytes, format="jpg")
plotImgBytes.seek(0)
plotImgStr = base64.b64encode(plotImgBytes.read()).decode()

# data for injecting into jinja2 template
context = {
    "reportDtStr": todayStr,
    "salesTblRows": salesTblRows,
    "topItemsRows": topItems,
    "salesBarChartImg": plotImgStr,
    "logoImg": logoImg,
    # "templatesFolderPath": pathlib.Path(os.path.abspath("templates")).as_uri(),
    # "bootstrapCss": requests.get("<https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css>").text,
    # "bootstrapJs": requests.get("<https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js>").text
}

# Step 2 - create jinja template object from file
template = jinja2.Environment(
    loader=jinja2.FileSystemLoader("./templates"),
    autoescape=jinja2.select_autoescape
).get_template("sales_report_template_bootstrap.html")

# Step 3 - render data in jinja template
reportText = template.render(context)

# Step 4 - Save genereate text as a HTML file
reportPath = "./reports/sales_report.html"
with open(reportPath, mode='w') as f:
    f.write(reportText)

# Step 5 - Convert html to pdf using pdfkit which is a wrapper of wkhtmltopdf
options = {
    "page-size": 'A4',
    "enable-local-file-access": True
}

pdfPath = "./reports/sales_report.pdf"
with open(reportPath) as f:
    pdfkit.from_file(f, pdfPath, options=options)

```

-   The HTML template in the above example uses bootstrap for CSS styling framework
-   The CSS and JS links can be local filesystem URLs (like `file:///C:/Users/James/jinja_python_reports/templates/bootstrap.min.css`) or external web URLs (like `https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css`)
-   To remove the dependency of external links from generated reports, the CSS and JS can be injected using style and script tags. For example the content of bootstrap CSS can be set a jinja variable string in python using `bootstrapCss = requests.get("<https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css>").text` and this content can be injected into the generated HTML using style tag as shown below. But while injecting external libraries, the autoescape option of jinja environment needs to be set to `False`

```html
<style>
    {{bootstrapCss}}
</style>

```

-   The generated HTML reports can be converted to pdf using `pdfkit` python module. pdfkit can be installed using `python -m pip install pdfkit`. As a dependency, wkhtmltopdf is to be installed. The installation procedure of wkhtmltopdf can be found at [](https://github.com/JazzCore/python-pdfkit/wiki/Installing-wkhtmltopdf#windows)[https://github.com/JazzCore/python-pdfkit/wiki/Installing-wkhtmltopdf#windows](https://github.com/JazzCore/python-pdfkit/wiki/Installing-wkhtmltopdf#windows)

### Output

![https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/jinja_html_report_bootstrap_demo.png?raw=true](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/jinja_html_report_bootstrap_demo.png?raw=true)

## Interactive HTML reports with JavaScript in jinja templates

### Python code

```python
# index.py file
import base64
import datetime as dt
import random
import jinja2

# Step 1 - create data for report
salesTblRows = []
for k in range(10):
    costPu = random.randint(1, 15)
    nUnits = random.randint(100, 500)
    salesTblRows.append({"sNo": k+1, "name": "Item "+str(k+1),
                         "cPu": costPu, "nUnits": nUnits, "revenue": costPu*nUnits})

topItems = [x["name"] for x in sorted(
    salesTblRows, key=lambda x: x["revenue"], reverse=True)][0:3]

todayStr = dt.datetime.now().strftime("%d-%b-%Y")

# create logo image from file
with open("templates/logo.png", "rb") as f:
    logoImg = base64.b64encode(f.read()).decode()

# data for injecting into jinja2 template
context = {
    "reportDtStr": todayStr,
    "salesTblRows": salesTblRows,
    "topItemsRows": topItems,
    "logoImg": logoImg,
}

# Step 2 - create jinja template object from file
template = jinja2.Environment(
    loader=jinja2.FileSystemLoader("./templates"),
    autoescape=jinja2.select_autoescape
).get_template("sales_report_template_plotly.html")

# Step 3 - render data in jinja template
reportText = template.render(context)

# Step 4 - Save genereate text as a HTML file
reportPath = "./reports/sales_report.html"
with open(reportPath, mode='w') as f:
    f.write(reportText)

```

### Jinja HTML Template

```html
<!-- templates/sales_report_template_plotly.html -->
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Report for {{reportDtStr}}</title>
    <style>
        body {
            margin: 2em;
            font-family: Arial, Helvetica, sans-serif;
        }

        table,
        th,
        td {
            border: 1px solid #555;
            border-collapse: collapse;
            padding: 0.25em;
        }
    </style>
    <script src="<https://cdn.plot.ly/plotly-2.26.0.min.js>" charset="utf-8"></script>
</head>

<body class="container">
    <img class="img-fluid" src="data:image/png;base64, {{logoImg}}" alt="logo"
        style="float: left; width:50px; height:50px; margin-right: 0.5em;">
    <div>
        <span>Daily sales report for {{reportDtStr}}</span><br>
        <span>Acme Inc.</span>
    </div>
    <hr>
    <div style="margin-top: 2em;"></div>
    <table class="table">
        <thead>
            <tr>
                <th>S.No</th>
                <th>Item Name</th>
                <th>Cost per Unit</th>
                <th>Units Sold</th>
                <th>Revenue </th>
            </tr>
        </thead>
        <tbody>
            {% for item in salesTblRows %}
            <tr>
                <td>{{item.sNo}}</td>
                <td>{{item.name}}</td>
                <td>{{item.cPu}}</td>
                <td>{{item.nUnits}}</td>
                <td>{{item.revenue}}</td>
            </tr>
            {% endfor %}
        </tbody>
    </table>

    <h2>Top performing items</h2>
    <ul class="list-group">
        {% for item in topItemsRows %}
        <li class="list-group-item">{{item}}</li>
        {% endfor %}
    </ul>
    <p style="page-break-after: always;">&nbsp;</p>
    <h2>Revenue Bar Chart</h2>
    <div id="revenueBarChart"></div>
    <script>
        var data = [{x: [], y: [], type: 'bar'}];

        {% for item in salesTblRows %}
        data[0].x.push("{{item.name}}");
        data[0].y.push("{{item.revenue}}");
        {% endfor %}

        Plotly.newPlot('revenueBarChart', data);  
    </script>
</body>

</html>

```

-   In this example, a JavaScript library `plotly.js` is used in the HTML template and a script is written in a script tag to initialize an interactive bar chart.
-   Bar chert data is set in the JavaScript code by substituting the values from python variables using jinja template for loop as shown below

```jsx
var data = [{x: [], y: [], type: 'bar'}];

{% for item in salesTblRows %}
data[0].x.push("{{item.name}}");
data[0].y.push("{{item.revenue}}");
{% endfor %}

Plotly.newPlot('revenueBarChart', data); 

```

### Output

![https://github.com/nagasudhirpulla/taming_python/blob/e5986e0883cdeead85a54b5b90139eb3ea939dee/blog/skills/assets/img/jinja_html_report_plotly_demo.png?raw=true](https://github.com/nagasudhirpulla/taming_python/blob/e5986e0883cdeead85a54b5b90139eb3ea939dee/blog/skills/assets/img/jinja_html_report_plotly_demo.png?raw=true)

## References

-   jinja docs - [](https://jinja.palletsprojects.com/en/3.1.x/api/#basics)[https://jinja.palletsprojects.com/en/3.1.x/api/#basics](https://jinja.palletsprojects.com/en/3.1.x/api/#basics)
-   Install wkhtmltopdf on windows - [](https://github.com/JazzCore/python-pdfkit/wiki/Installing-wkhtmltopdf#windows)[https://github.com/JazzCore/python-pdfkit/wiki/Installing-wkhtmltopdf#windows](https://github.com/JazzCore/python-pdfkit/wiki/Installing-wkhtmltopdf#windows)
-   [](https://linlinzhao.com/tech/2021/01/20/jinja-report.html)[https://linlinzhao.com/tech/2021/01/20/jinja-report.html](https://linlinzhao.com/tech/2021/01/20/jinja-report.html)
-   [](https://stackoverflow.com/a/70881619/2746323)[https://stackoverflow.com/a/70881619/2746323](https://stackoverflow.com/a/70881619/2746323)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTM4Njg0MDYxNV19
-->