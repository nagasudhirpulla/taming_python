python notes -  http://thomas-cokelaer.info/tutorials/python/basics.html#the-basics

matplotlib overview tutorial - https://towardsdatascience.com/data-visualization-using-matplotlib-16f1aae5ce70


### TODOS
* matplotlib save all plots in a pdf
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
eyJoaXN0b3J5IjpbLTM2NDU4ODEzNiwtMTYwNzU1NjQ2OCwtMT
E5Mzk4OTg3MCw5OTA1MTMxMTEsLTg4MTEzODM4MSwtOTg5NDc3
MjYxLC0yMDU2NDA1NTUwLC05Nzg2NzM0MSwtMzIzOTg4MTQ5LC
0xOTIzNzYzOTQ3LDM5NDUzNzg2OSwtMTM5MTQ5NTYwNSwtMjIx
ODg5OTc1LDY2MTY3NDAxNCw5MjY3OTUzMDQsLTM5ODU0MjYwMC
wxMTcyMjM2MjgzLDE4NTIwMDYwMjUsMjEyMTU3NzE0LC03NzQ4
NjAxNDNdfQ==
-->