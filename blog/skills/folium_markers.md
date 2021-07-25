## Skill - Draw markers in python folium maps

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [Introduction to Folium for interactive maps in python](https://nagasudhir.blogspot.com/2021/07/introduction-to-folium-for-interactive.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision
<hr/>

In this post we will learn how to draw markers on a folium map in python

 See [this](https://nagasudhir.blogspot.com/2021/07/introduction-to-folium-for-interactive.html) post to learn about folium libary basics

### Create a simple marker
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

<hr/>

### References
* GeckoDriver for firefox - https://github.com/mozilla/geckodriver/releases
* Selenium Docs - https://selenium-python.readthedocs.io/getting-started.html

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyODAzOTEyMTldfQ==
-->