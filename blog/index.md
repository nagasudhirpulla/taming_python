Hey Guys

I just wanted to create a tutorial series that helps people develop skill sets in python to achieve their data manipulation / visualization goals

The approach is to create a nested tree of skills to achieve all the steps to achieve each specific goal

For example, if 

Goal = Read csv file, plot all columns data one below the other, save plot as a PNG image, 

User story = Create a summary image of voltage time-series from a csv file 

The steps and skill sets required may be

Steps
-----
* read excel file into pandas dataframe
* get the shape/dimensions of a dataframe
* get all the column names of dataframe
* create a figure with matplotlib subplots as the number of dataframe columns
* Set title to the figure
* iterate through all columns data of dataframe
* plot each dataframe column data inside the generated axis handles with axis title, legend and axis labels included

Skill sets
----------
using tight layout to optimize plot space in a matplotlib plot (#18) (requires #1, #3, #4, #15, #16, #17)

set plot title, plot size in inches in a matplotlib plot (#19) (requires #1, #3, #4, #15, #16)

set subplot title, x and y axis labels in a matplotlib plot (#20) (requires #1, #3, #4, #15, #16, #17)

enable legends for an axis handle / subplot in matplotlib plot (#21) (requires #1, #3, #4, #15, #16)

save plot image as a PNG/PDF/JPG/SVG file using savefig function (#22) (requires #1, #3, #4, #15, #16)

---manipulating variables (#5) (requires #1)

---create arrays with sequences (#6) (requires #1)

---'range' function to create sequences for using inside a 'for' loop (#7) (requires #1)

---'for' loop (#8) (requires #1)

---anatomy/nomenclatures of a pandas dataframe (#9) (requires #1, #2, #4)

---create dataframe from array of objects (#10) (requires #1, #2, #4, #9)

---create dataframe from object with each property as array (#11) (requires #1, #2, #4, #9)

---read excel file into pandas dataframe (#12) (requires #1, #2, #4, #9)

---get the shape/dimension of a dataframe (#13) (requires #1, #2, #4, #9)

---get all the column names of dataframe (#14) (requires #1, #2, #4, #9)

---anatomy/nomenclatures of a plot in matplotlib (#15) (requires #1, #3, #4)

---basic data plotting in matploltlib using matploltlib.pyplot (#16) (requires #1, #3, #4, #15)

---creating figure and axis handles to plot multiple subplots in matplotlib (#17) (requires #1, #3, #4, #15)

------setup python development environment (#1)

------install pandas library (#2)

------install matplotlib library (#3)

------import required library modules for using in our python programs (#4)

* Each skill mentioned above will have a blog post, sample code and references
* We can see that the user is now clear on what skills to acquire in order to achieve a specific goal
* This way the user will be motivated to learn the basics (which generally is boring, without knowing the purpose)
* We can also have a knowledge base of code samples which can help many beginners

Skills database is maintained as a google spreadsheet at https://docs.google.com/spreadsheets/d/1vsw5TSprGmex4k6aNvWiAmGOYAH9RU80OpUFMg9Ahvs/edit?usp=sharing
<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoiZXh0ZW5zaW9uczpcbiAgcHJlc2V0Oi
AnJ1xudGl0bGU6IEludHJvIHRvIFRhbWluZyBQeXRob24gc2Vy
aWVzXG5hdXRob3I6IE5hZ2FzdWRoaXIgUHVsbGFcbnRhZ3M6IC
dweXRob24sIHR1dG9yaWFsJ1xuY2F0ZWdvcmllczogJ2xlYXJu
aW5nLCBweXRob24sIHR1dG9yaWFsJ1xuZGF0ZTogJzIwMjAtMD
QtMTQnXG4iLCJoaXN0b3J5IjpbLTEwNTE4OTcyMzAsLTYzNjA4
ODk5Miw3MzA5OTgxMTZdfQ==
-->