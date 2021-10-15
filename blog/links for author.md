python notes -  http://thomas-cokelaer.info/tutorials/python/basics.html#the-basics

matplotlib overview tutorial - https://towardsdatascience.com/data-visualization-using-matplotlib-16f1aae5ce70


### TODOS
* process dataframes and dbf in chunks
* docxtpl tutorial for templates, plots, images etc
```python
import datetime as dt
import random

from docx2pdf import convert
import matplotlib.pyplot as plt
from docxtpl import DocxTemplate, InlineImage

# create a document object
doc = DocxTemplate("reportTmpl.docx")

salesTblRows = []
topItems = []
for k in range(10):
    costPu = random.randint(1, 15)
    nUnits = random.randint(100, 500)
    salesTblRows.append({"sNo": k+1, "name": "Item "+str(k+1),
                         "cPu": costPu, "nUnits": nUnits, "revenue": costPu*nUnits})

topItems = [x["name"] for x in salesTblRows]
random.shuffle(topItems)
topItems = topItems[0:3]

todayStr = dt.datetime.now().strftime("%d-%b-%Y")

# create context dictionary
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
convert(reportWordPath, reportWordPath.replace(".docx", ".pdf"))
```
* Histogram in python
* Manage application configuration or application secrets in Excel  
* global variables and using them inside functions- https://instructobit.com/tutorial/108/How-to-share-global-variables-between-files-in-Python
* python subprocess communication - https://eli.thegreenplace.net/2017/interacting-with-a-long-running-child-process-in-python/
* rounding of decimals while printing and rounding the number itself
* flask server basics
* naming conventions for classes (nouns), variables (nouns), functions (verbs), using camel case, avoid obvious names and use contextual names for better readability



<!--stackedit_data:
eyJoaXN0b3J5IjpbNzk1NzYzMzM1LC02NTY3Mzc5OTcsLTE2Mz
IzOTIwODcsLTIyOTYyOTU1NywxOTI0MjYzOTg4LDEzOTEzOTQw
NjAsMTI1ODI4NjIzNywtODkwMjM5MTAwLC0xMTQ0OTExNDM3LC
0zNjQ1ODgxMzYsLTE2MDc1NTY0NjgsLTExOTM5ODk4NzAsOTkw
NTEzMTExLC04ODExMzgzODEsLTk4OTQ3NzI2MSwtMjA1NjQwNT
U1MCwtOTc4NjczNDEsLTMyMzk4ODE0OSwtMTkyMzc2Mzk0Nywz
OTQ1Mzc4NjldfQ==
-->