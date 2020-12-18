## Skill - Inducing time delays in python scripts using 'sleep' function in time module
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup Python Development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Commenting in python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Basic printing in python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr/>

Using the `sleep` function in time module, we can make the code execution delayed by a desired time interval

![sleep_illustration](https://raw.githubusercontent.com/nagasudhirpulla/taming_python/master/blog/skills/assets/img/sleep_illustration.png)

### Function Usage
First import the `time` module
To induce a delay of say 5 seconds in your code, just call `time.delay(5)`

### Example
```python
import time
print("Hello ")
time.sleep(2)
print("World!")
# this prints 'Hello ' first waits 2 seconds and then prints 'World!'
```

### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://pynative.com/online-python-code-editor-to-execute-python-code/ or https://repl.it/repls/MountainousWhirlwindRatios

### You can practice here
<iframe height="800px" width="100%" src="https://repl.it/repls/AcclaimedIndigoSet?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

### References
* image credits - https://realpython.com/python-sleep/

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IEluZHVjaW5nIHRpbWUgZG
VsYXlzIGluIHB5dGhvbiB1c2luZyBzbGVlcCBmdW5jdGlvblxu
YXV0aG9yOiBOYWdhc3VkaGlyIFB1bGxhXG5kYXRlOiAnMjAyMC
0wNS0yNCdcbnRhZ3M6ICdsZWFybmluZywgcHl0aG9uLCB0YW1p
bmdfcHl0aG9uX3NraWxsJ1xuY2F0ZWdvcmllczogdGFtaW5nX3
B5dGhvbl9za2lsbFxuIiwiaGlzdG9yeSI6WzE3MDYxNDkyNjQs
LTE3MDk0MDgzMSwtMzQxNDg1ODUwXX0=
-->