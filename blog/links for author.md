python notes -  http://thomas-cokelaer.info/tutorials/python/basics.html#the-basics

matplotlib overview tutorial - https://towardsdatascience.com/data-visualization-using-matplotlib-16f1aae5ce70


### TODOS
* matplotlib save all plots in a pdf
```python
from matplotlib.backends.backend_pdf import PdfPages
import matplotlib.pyplot as plt
import random

pdfFile = PdfPages("output.pdf")

for pltItr in range(10):
    # data for plot
    xVals = [x for x in range(1, 11)]
    yVals = [random.randint(50, 100) for x in xVals]

    # create a plot
    fig, ax = plt.subplots()
    la, = ax.plot(xVals, yVals)
    ax.set_title("Plot number {0}".format(pltItr+1))
    ax.set_xlabel("X Values")
    ax.set_ylabel("Y Values")

    # add figure to pdf file
    pdfFile.savefig(fig, bbox_inches='tight')

# close the pdf file
pdfFile.close()
```
* matplotlib legend at the bottom of plot
```python
# %%
import pandas as pd
import matplotlib.pyplot as plt
import matplotlib.backends.backend_pdf
import matplotlib
# %%
dfOnbar = pd.read_excel("input.xlsx", sheet_name="DCOnbar", index_col=0)
dfOnbar = dfOnbar[range(1, 97)]

dfSch = pd.read_excel("input.xlsx", sheet_name="Schedule", index_col=0)
dfSch = dfSch[range(1, 97)]

dfTm = pd.read_excel("input.xlsx", sheet_name="TechMin", index_col=0)
dfTm = dfTm[range(1, 97)]

dfOptSch = pd.read_excel("input.xlsx", sheet_name="Result Report", index_col=0)
dfOptSch = dfOptSch[range(1, 97)]
# %%
# get the list of generators
gens = dfOnbar.index.tolist()

# create a plot for each generator
pdf = matplotlib.backends.backend_pdf.PdfPages(r"plots\output.pdf")
for targetGen in gens:
    fig, ax = plt.subplots()
    # set plot title
    ax.set_title(targetGen)

    # set x and y labels
    ax.set_xlabel('Time Block')
    ax.set_ylabel('MW')

    # plot onbar DC
    la1, = ax.plot(list(range(1, 97)), dfOnbar.loc[targetGen], color='orange')
    la1.set_label('Onbar')

    # plot Technical Minimum
    la2, = ax.plot(list(range(1, 97)), dfTm.loc[targetGen], color='green')
    la2.set_label('Tech. Min')

    # plot Original Schedule
    la3, = ax.plot(list(range(1, 97)), dfSch.loc[targetGen], color='blue')
    la3.set_label('Original Schedule')

    # plot Optimal Schedule
    la4, = ax.plot(list(range(1, 97)),
                   dfOptSch.loc[targetGen], color='magenta')
    la4.set_label('Optimal Schedule')

    # Put a legend below current axis
    ax.legend(loc='upper center', bbox_to_anchor=(0.5, -0.15),
                    fancybox=True, shadow=True, ncol=3)

    fig.savefig(r"plots\{0}.png".format(targetGen), bbox_inches='tight')
    pdf.savefig(fig, bbox_inches='tight')

pdf.close()
# %%
```
bbox_to_legend guide - https://jdhao.github.io/2018/01/23/matplotlib-legend-outside-of-axes/
* docxtpl tutorial for templates, plots, images etc
* Histogram in python
* Manage application configuration or application secrets in Excel  
* global variables and using them inside functions- https://instructobit.com/tutorial/108/How-to-share-global-variables-between-files-in-Python
* python subprocess communication - https://eli.thegreenplace.net/2017/interacting-with-a-long-running-child-process-in-python/
* rounding of decimals while printing and rounding the number itself
* flask server basics
* naming conventions for classes (nouns), variables (nouns), functions (verbs), using camel case, avoid obvious names and use contextual names for better readability



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTExNDQ5MTE0MzcsLTM2NDU4ODEzNiwtMT
YwNzU1NjQ2OCwtMTE5Mzk4OTg3MCw5OTA1MTMxMTEsLTg4MTEz
ODM4MSwtOTg5NDc3MjYxLC0yMDU2NDA1NTUwLC05Nzg2NzM0MS
wtMzIzOTg4MTQ5LC0xOTIzNzYzOTQ3LDM5NDUzNzg2OSwtMTM5
MTQ5NTYwNSwtMjIxODg5OTc1LDY2MTY3NDAxNCw5MjY3OTUzMD
QsLTM5ODU0MjYwMCwxMTcyMjM2MjgzLDE4NTIwMDYwMjUsMjEy
MTU3NzE0XX0=
-->