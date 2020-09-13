## Challenge - Implement RS flip-flop logic using if statement and variables
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [Boolean and Logical Operations on variables in Python](https://nagasudhir.blogspot.com/2020/04/operations-on-variables-in-python.html)
* ['if', 'else', 'elif' condition in python](https://nagasudhir.blogspot.com/2020/04/if-condition-in-python_14.html)

Please make sure to go through all the skills mentioned above to understand and execute the steps mentioned below

<hr/>

### Truth table of RS flip-flop
In order to implement an RS flip-flop, we need to implement its truth table
![rs_flipflop_truth_table](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/goals/assets/img/rs_flipflop_truth_table.jpg)
### Python implementation of RS flip-flop
* We will use 4 variables to store and manipulate the values of 2 inputs, current state and next state
```python
# storing initial states and inputs in variables
inp1 = 0
inp2 = 1
prevState = 1
nextState = None

# RS flip-flop truth table implementation
if inp1==0 and inp2==0:
	nextState = prevState
elif inp1==0 and inp2==1:
	nextState = 0
elif inp1==1 and inp2==0:
	nextState = 1
else:
	print('Invalid input provided')
	nextState = None

if nextState != None:
	print("The next state is {0}".format(nextState))
else:
	print("Unable to produce next state, please provide valid inputs and states...")

print("Execution complete...")
```
* Run the code using menu _Run -> Run Without Debugging_
* You should see the following output
```
The next state is 0
Execution complete...
```
You can also change the variable values and execute to see different outputs printed in the console

### Video
The video for this post can be found [here](https://youtu.be/Os7ppbJh4To)

<iframe width="560" height="315" src="https://www.youtube.com/embed/Os7ppbJh4To" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### You can practice here
<iframe height="800px" width="100%" src="https://repl.it/repls/BowedUnusualWheel?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)
<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IEltcGxlbWVudCBSUyBmbG
lwLWZsb3AgbG9naWMgdXNpbmcgaWYgc3RhdGVtZW50IGFuZCB2
YXJpYWJsZXNcbmF1dGhvcjogTmFnYXN1ZGhpciBQdWxsYVxuZG
F0ZTogJzIwMjAtMDctMTUnXG50YWdzOiAncHl0aG9uLCBsZWFy
bmluZywgdGFtaW5nX3B5dGhvbl9nb2FsJ1xuY2F0ZWdvcmllcz
ogdGFtaW5nX3B5dGhvbl9nb2FsXG4iLCJoaXN0b3J5IjpbMTQ3
NTE4ODM4MiwtOTE0ODM4MjAsLTMyMDc1MjQwLC01NTkwOTE2Nj
YsLTE3OTYwNDU2NTgsLTUzNjg3MjkzN119
-->