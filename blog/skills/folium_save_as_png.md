## Skill - Save folium map as a png image using selenium browser automation

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [Introduction to Folium for interactive maps in python](https://nagasudhir.blogspot.com/2021/07/introduction-to-folium-for-interactive.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision
<hr/>

In this post we will learn how to save folium map as a pang image using selenium browser automation.

 See [this](https://nagasudhir.blogspot.com/2021/07/introduction-to-folium-for-interactive.html) post to learn about folium libary basics

### Prerequisites - Selenium setup
In order to perform browser automation for this task we need the following components
* selenium python module - This can be installed using the command 
```python -m pip install selenium```
* Gecko driver - This is used by selenium library to open firefox browser. Download the executable from [here](https://github.com/mozilla/geckodriver/releases) and keep the exe file in the same location as the python file. 
Alternatively, you can place the exe file at some folder location and add that folder location to the **PATH** variable of the system.


### Code to save the html file as png using selenium
```python
mapFname = 'output.html'
mapUrl = 'file://{0}/{1}'.format(os.getcwd(), mapFname)

# download gecko driver for firefox from here - https://github.com/mozilla/geckodriver/releases

# use selenium to save the html as png image
driver = webdriver.Firefox()
driver.get(mapUrl)
# wait for 5 seconds for the maps and other assets to be loaded in the browser
time.sleep(5)
driver.save_screenshot('output.png')
driver.quit()
```

### Example code
```python
import folium
from selenium import webdriver
import os
import time

# create a map object with a desired initial map center and initial map zoom
mapObj = folium.Map(location=[24.2170111233401, 81.0791015625000],
                    zoom_start=5)

# draw some circles
circlesData = [
    [25, 74, 80000],
    [22, 79, 60000],
    [26, 82, 90000]
]

for d in circlesData:
    folium.Circle(radius=d[2],
                  location=[d[0], d[1]],
                  fill=True,
                  stroke=False,
                  fill_opacity=0.6,
                  ).add_to(mapObj)

# save the map as html
mapFname = 'output.html'
mapObj.save(mapFname)

mapUrl = 'file://{0}/{1}'.format(os.getcwd(), mapFname)

# download gecko driver for firefox from here - https://github.com/mozilla/geckodriver/releases

# use selenium to save the html as png image
driver = webdriver.Firefox()
driver.get(mapUrl)
# wait for 5 seconds for the maps and other assets to be loaded in the browser
time.sleep(5)
driver.save_screenshot('output.png')
driver.quit()
```

if you prefer to use selenium with chrome, download Chrome WebDriver from https://sites.google.com/a/chromium.org/chromedriver/downloads

### Video
The video for this post can be found [here](https://youtu.be/RL-phs5FnmU)
<iframe width="560" height="315" src="https://www.youtube.com/embed/RL-phs5FnmU" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<hr/>

### References
* GeckoDriver for firefox - https://github.com/mozilla/geckodriver/releases
* Selenium Docs - https://selenium-python.readthedocs.io/getting-started.html

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTc3NDAzMzU1MiwtMTU1ODc3Mjg5OCwtND
E0Nzk0NjYyLDkzNTIyMDU1Nyw4ODUwNDczNDhdfQ==
-->