## Skill - Directory Listing in Flask

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Flask python module introduction](https://nagasudhir.blogspot.com/2022/04/flask-python-module-introduction-for.html)
* [Serve static files in flask](https://nagasudhir.blogspot.com/2022/04/serve-static-files-in-flask.html)
* [Flask jinja templating](https://nagasudhir.blogspot.com/2022/04/jinja-templates-in-flask.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr/>

* In this post we will learn how show a list of files present in the server directory along with navigation and download features using Flask
 
 ![flask_directory_listing](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/flask_directory_listing.png)
 

## Use Cases
* Directory listing may be useful if we desire to display files of a particular folder in a server like generated reports, images etc. 

## Basic server
* The following python server acts as a flask server that runs on port 50100
* We will add the directory listing to this server
```py
from flask import Flask

# create a server instance
app = Flask(__name__)

@app.route('/')
def index():
    return "Hello World!!!"

# run the server
app.run(host="0.0.0.0", port=50100, debug=True)
```

### Get all the folder contents using os.scandir
* For a given folder path, all the files and folder inside the folder can be fetched using the `os.scandir` function
```py
import os
folderPath = r"C:\Windows"
print([x.name for x in os.scandir(folderPath)])
```

### Get the file size and modified time with os.stat
* The file size and last modified time for a file path can be derived from `os.stat` function
```py
import os

filePath = r'C:\Windows\regedit.exe'
fileStat = os.stat(filePath)

print(f"fileSize = {fileStat.st_size} bytes")
print(f"Modified Time in posix timestamp = {fileStat.st_mtime}")
```
* We can use helper functions to make the file size (in bytes) and modified time (POSIX timestamp) more readable as shown in the below example

```py
import os
import datetime as dt

def getReadableByteSize(num, suffix='B') -> str:
    for unit in ['', 'K', 'M', 'G', 'T', 'P', 'E', 'Z']:
        if abs(num) < 1024.0:
            return "%3.1f%s%s" % (num, unit, suffix)
        num /= 1024.0
    return "%.1f%s%s" % (num, 'Yi', suffix)


def getTimeStampString(tSec: float) -> str:
    tObj = dt.datetime.fromtimestamp(tSec)
    tStr = dt.datetime.strftime(tObj, '%Y-%m-%d %H:%M:%S')
    return tStr

filePath = r'C:\Windows\regedit.exe'
fileStat = os.stat(filePath)

print(f"fileSize = {getReadableByteSize(fileStat.st_size)} bytes")
print(f"Modified Time in posix timestamp = {getTimeStampString(fileStat.st_mtime)}")
```

### Deriving file path from URL using safe_join 
* The path of the file is expressed as a URL path in directory listing
* Path of the desired file in the file system can be derived using this URL path just by joining the base folder path with the URL path 
* For example, if the request URL was `/Web/Screen/img102.jpg` and the base folder is located at  `C:\Abcd`, the desired file path would be `C:\Abcd\Web\Screen\img102.jpg`
* This can be achieved using `safe_join` function from flask as shown below
```py
from flask import safe_join
urlPath = 'Web/Screen/img102.jpg'
baseFolderPath = r'C:\Abcd'
print('filePath=',safe_join(baseFolderPath, urlPath).replace('\\', '/'))
```
* The advantage of using `safe_join` over `os.path.join` is that it ensures that files above the server base folder are not served. Hence a security issue can be addressed using safe_join function

### Get parent folder path of a folder using pathlib
* For navigational purposes, we need to create a link for the parent folder of the current folder being displayed
* This can be derived using the Path object from pathlib library as shown below
```py
from pathlib import Path

folderPath = r'C:\Windows\Containers\serviced'
print('parent folder = ', Path(folderPath).parents[0])
```

### Get file or folder path relative to base folder using os.path.relpath
* Paths relative to the base server folder are required to make the file or folder clickable in the directory listing
* This can be achieved using the os.path.relpath as shown below
```py
import os

filePath = r'C:\Windows\Containers\serviced\abcd.txt'
baseFolderPath = r'C:\Windows'

print('realtive path = ', os.path.relpath(filePath, baseFolderPath).replace("\\", "/"))
```

### check if a file or folder exists using os.path.exists function
* When a user clicks on a file or folder, the URL can be resolved in to an absolute path at the server
* The file or folder path needs to be checked if exists or not. This can be done using `os.path.isdir` as shown below.
```py
import os

filePath = r"C:\abcd\xyz.txt"
print("file exists? = ", os.path.exists(filePath))
```

### check if a path is a folder using os.path.isdir function
* When a user clicks on a file or folder, the URL can be resolved in to an absolute path at the server
* The function `os.path.isdir` can be used to determine if a path is a folder or a file as shown below
```py
import os

filePath = r"C:\Windows\Branding\Basebrd\basebrd.dll"
print("isdir for file = ", os.path.isdir(filePath))

folderPath = r"C:\Windows\Branding\Basebrd"
print("isdir for folder = ", os.path.isdir(folderPath))
``` 

### Download file using flask send_file function
* To make the file downloadable upon on clicking on the link, the whole file needs to be sent to the browser from the server instead of a page.
* This can be done using the send_file function from flask as shown below
```py
from flask import Flask, send_file

# create a server instance
app = Flask(__name__)

@app.route('/')
def index():
    filePath = r"C:\Abcd\xyz.txt"
    return send_file(filePath)

app.run(host="0.0.0.0", port=50100, debug=True)
```

## Putting all of it together
* Using all the above functions we can create a server that can perform directory listing as shown below

```py
# server python file
from flask import Flask, render_template, abort, safe_join, send_file
from pathlib import Path
import os
import datetime as dt

# create a server instance
app = Flask(__name__)
FolderPath = r"C:\Users\Nagasudhir\Downloads"

@app.route('/')
def index():
    return "Hello World!!!"

def getReadableByteSize(num, suffix='B') -> str:
    for unit in ['', 'K', 'M', 'G', 'T', 'P', 'E', 'Z']:
        if abs(num) < 1024.0:
            return "%3.1f%s%s" % (num, unit, suffix)
        num /= 1024.0
    return "%.1f%s%s" % (num, 'Y', suffix)

def getTimeStampString(tSec: float) -> str:
    tObj = dt.datetime.fromtimestamp(tSec)
    tStr = dt.datetime.strftime(tObj, '%Y-%m-%d %H:%M:%S')
    return tStr

def getIconClassForFilename(fName):
    fileExt = Path(fName).suffix
    fileExt = fileExt[1:] if fileExt.startswith(".") else fileExt
    fileTypes = ["aac", "ai", "bmp", "cs", "css", "csv", "doc", "docx", "exe", "gif", "heic", "html", "java", "jpg", "js", "json", "jsx", "key", "m4p", "md", "mdx", "mov", "mp3",
                 "mp4", "otf", "pdf", "php", "png", "pptx", "psd", "py", "raw", "rb", "sass", "scss", "sh", "sql", "svg", "tiff", "tsx", "ttf", "txt", "wav", "woff", "xlsx", "xml", "yml"]
    fileIconClass = f"bi bi-filetype-{fileExt}" if fileExt in fileTypes else "bi bi-file-earmark"
    return fileIconClass

# route handler
@app.route('/reports/', defaults={'reqPath': ''})
@app.route('/reports/<path:reqPath>')
def getFiles(reqPath):
    # Join the base and the requested path
    # could have done os.path.join, but safe_join ensures that files are not fetched from parent folders of the base folder
    absPath = safe_join(FolderPath, reqPath)

    # Return 404 if path doesn't exist
    if not os.path.exists(absPath):
        return abort(404)

    # Check if path is a file and serve
    if os.path.isfile(absPath):
        return send_file(absPath)

    # Show directory contents
    def fObjFromScan(x):
        fileStat = x.stat()
        # return file information for rendering
        return {'name': x.name,
                'fIcon': "bi bi-folder-fill" if os.path.isdir(x.path) else getIconClassForFilename(x.name),
                'relPath': os.path.relpath(x.path, FolderPath).replace("\\", "/"),
                'mTime': getTimeStampString(fileStat.st_mtime),
                'size': getReadableByteSize(fileStat.st_size)}
    fileObjs = [fObjFromScan(x) for x in os.scandir(absPath)]
    # get parent directory url
    parentFolderPath = os.path.relpath(
        Path(absPath).parents[0], FolderPath).replace("\\", "/")
    return render_template('files.html.j2', data={'files': fileObjs,
                                                 'parentFolder': parentFolderPath})

# run the server
app.run(host="0.0.0.0", port=50100, debug=True)
```

## Workflow
The workflow to serve the directory listing page would be as follows
* Extract the relative path from URL
* Derive the absolute path w.r.t the base folder using relative path
* If the derived path is a valid file, send the file
* If the derived path is a folder path, serve a directory listing page that displays the list of files and folders in the folder
* While displaying the folder contents, each file or folder is given a hyperlink which sends the request to the server to serve its contents. Also a link to parent directory will be provided for easy navigation

### Template file
```html
<!--Template file-->
<!--templates/files.html.j2-->
<h2>Directory Listing Example</h2>
<table class="table table-striped table-responsive">
    <thead>
        <tr>
            <th>Name</th>
            <th>Modified Time</th>
            <th>Size</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <a href="{{ url_for('getFiles', reqPath=data['parentFolder']) }}">
                    <span><i class="bi bi-folder-symlink" style="margin-right:0.3em"></i>Parent Directory</span>
                </a>
            </td>
            <td></td>
            <td></td>
        </tr>
        {% for fileObj in data['files'] %}
        <tr>
            <td>
                <a href="{{ url_for('getFiles', reqPath=fileObj['relPath']) }}">
                    <span><i class="{{fileObj['fIcon']}}" style="margin-right:0.3em"></i>{{ fileObj['name'] }}</span>
                </a>
            </td>
            <td>{{fileObj['mTime']}}</td>
            <td>{{fileObj['size']}}</td>
        </tr>
        {% endfor %}
    </tbody>
</table>

<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.9.1/font/bootstrap-icons.css">

<style>
table {table-layout:fixed; width:100%;}
table td, th {word-wrap:break-word;}
th {text-align: left;}
</style>
```


### Video
The video for this post can be seen [here](https://youtu.be/x4HkFdBVVrw)

<iframe width="560" height="315" src="https://www.youtube.com/embed/x4HkFdBVVrw" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## References
* Flask quickstart - https://flask.palletsprojects.com/en/2.1.x/quickstart/
* Jinja docs - https://jinja.palletsprojects.com/en/3.1.x/templates/
* os.scandir - https://docs.python.org/3/library/os.html#os.scandir
* os.stat - https://docs.python.org/3/library/stat.html
* flask safe_join - https://tedboy.github.io/flask/generated/flask.safe_join.html
*  Pathlib parents - https://docs.python.org/3/library/pathlib.html#pathlib.PurePath.parents
* os.path.repath - https://docs.python.org/3/library/os.path.html#os.path.relpath
* flask send_file - https://tedboy.github.io/flask/generated/flask.send_file.html
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4NDAyNTAyMzAsLTE1OTU4OTUwMDMsLT
EyNzM1MjQ0MiwtODE2NjA1OTUwLC05OTEyMTAwNTgsLTIzNjEw
MDQyOSwtMTQyNzUzNDkwMSwtMTU0NDI5MDUxLDE2MjQzMTM3Nz
IsMTQ0Mjk3ODU0MywxNjU0MDg1MjQwLDE0OTA0NDcyNjgsLTE1
NDY5Mjg1MTUsLTE4MzYwNDQ1MDMsLTE5MzE2MTMwODgsLTEyNT
c0MTY4NDldfQ==
-->