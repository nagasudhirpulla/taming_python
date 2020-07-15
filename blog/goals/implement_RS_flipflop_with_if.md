## Challenge - Implement RS flip-flop logic with if statement
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
	print("The nextstate is {0}".format(nextState))
else:
	print("Unable to produce next state, please provide valid inputs and states...")

print("Execution complete...")
```
* Run the code using menu _Run -> Run Without Debugging_
* You should see 
```

```
printed in the terminal

### You can practice here
<iframe height="800px" width="100%" src="https://repl.it/repls/FondNutritiousParticle?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)
<!--stackedit_data:
eyJoaXN0b3J5IjpbOTI3MzQzNTkzLC05MTQ4MzgyMCwtMzIwNz
UyNDAsLTU1OTA5MTY2NiwtMTc5NjA0NTY1OCwtNTM2ODcyOTM3
XX0=
-->