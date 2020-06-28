## Skill - Using Jupyter Notebooks in Visual Studio Code
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision
<hr/>
In this post we are going to learn about how to use jupyter notebooks and add jupyter notebook features to python files in Visual Studio Code

![jupyter_notebook_in_vs_code](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/jupyter_notebook_in_vs_code.png)
## Why the Jupyter Notebooks approach
* Jupyter notebooks is the way to go approach for experimenting and debugging with python code or execute code in small parts while developing it.
* Each part of a code is called a **cell** in a Jupyter notebook
* Jupyter notebooks can also be used to graphically visualize the variables using the variable explorer.
* One more use case of jupyter notebooks is that you can load data into variables once, and then play with them as many times as you wish by changing the code. 
This is particularly useful if you load huge data into your variables

## Add Jupyter notebook features to existing python code
![jupyter_notebook_py_file](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/jupyter_notebook_py_file.png)
* As shown in the image above, just add `# %%` in the line above  your code to make it a jupyter notebook cell
* The cell controls like Run Cell, Run Above will automatically displayed by Visual Studio Code
* Upon  running the cells in python file, we will get to see output in the right-side output pane. An example image is shown below
![jupyter_notebook_kernel_output](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/jupyter_notebook_kernel_output.png)
## Variable Explorer to examine the variables graphically 
* Once the code cells are executed, the variables will be persisted
* These can be seen graphically using the variable explorer button as shown in the below image
![jupyter_notebook_variable_explorer](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/jupyter_notebook_variable_explorer.PNG)
* Variable Explorer is very handy if you want to examine the variables in the middle of complete code execution, just like debugging

## Using jupyter notebooks in Visual Studio Code
* Jupyter Notebooks are saved with `.ipynb` extension
* To create a new ipynb file, open command pallete using `Ctrl+Shift+P` and select the command `Create New Blank Jupyter Notebook`
![jupyter_notebook_create_new](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/jupyter_notebook_create_new.PNG)* The cell user interface controls of ipynb file are shown in the below image
![jupyter_notebook_ipynb_file](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/jupyter_notebook_ipynb_file.png)* Even plotting outputs are displayed in the cell output section. An example cell output with plots can be seen in the image below
![jupyter_notebook_inline_output](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/jupyter_notebook_inline_output.png)
## Convert a jupyter notebook to a python file
* Open a jupyter notebook ipynb file in Visual Studio Code
* Click the 'convert and save to python' button as shown in the image below
![jupyter_notebook_convert_to_python](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/jupyter_notebook_convert_to_python.PNG)
<hr/>

### References
* Official tutorial page - https://code.visualstudio.com/docs/python/jupyter-support?ocid=AID2463683&wt.mc_id=ai-c9-sejuare
* Video by Microsoft - https://youtu.be/_C0vbLV6WdA 

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)


<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IFVzaW5nIEp1cHl0ZXIgTm
90ZWJvb2tzIGluIFZpc3VhbCBTdHVkaW8gQ29kZVxuYXV0aG9y
OiBOYWdhc3VkaGlyIFB1bGxhXG5kYXRlOiAnMjAyMC0wNi0yOC
dcbnRhZ3M6ICdweXRob24sIGxlYXJuaW5nLCB0dXRvcmlhbCwg
dGFtaW5nX3B5dGhvbl9za2lsbCdcbmNhdGVnb3JpZXM6IHRhbW
luZ19weXRob25fc2tpbGxcbiIsImhpc3RvcnkiOlsxOTU2Njkx
MDA3LC0xOTQzOTUxOTkwLC04MzUxMjIyODQsNDQwNzUwNTc0LC
0xNTc0MjIyNDUwLC01NDA1MTMyOTJdfQ==
-->