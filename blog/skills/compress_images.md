# Compress photos in bulk with pillow python module
-   Images can be compressed to reduce storage space. This can be particularly useful while storing images in cloud storage.
-   Images can be compressed or resized using `pillow` python library in python. It can be installed using pip with the command `python -m pip install Pillow`
-   Pillow is a python library for image processing
-   To reduce the size of an image, it can be resized to lower resolution or jpeg compression can be increased
-   `thumbnail` function of pillow library can be used to resize an image.
-   `save` function of pillow library can be used to control the jpeg image file compression percentage
-   `piexif` python library can be used to extract the exif data (device, gps, etc) of the original image and use it in the compressed file
-   The source code below compresses the images in the folder `D:\\test1` and saves the compressed images in `D:\\test2`. The file metadata like modified time and last access time is set in the compressed image using the `os.stat` and `os.utime` functions

```python
import os
from PIL import Image
import piexif
import glob
import pathlib

def copyMetadata(srcImgPath, destImgPath):
    # Open the source image
    srcImg = Image.open(srcImgPath)

    # Extract EXIF data from the source image
    exifData = piexif.load(srcImg.info['exif'])

    # bug handling for 41729 exif tag (scenetype)
    if 41729 in exifData['Exif'] and isinstance(exifData['Exif'][41729], int):
        exifData['Exif'][41729] = str(exifData['Exif'][41729]).encode('utf-8')

    # Open the destination image
    destImg = Image.open(destImgPath)

    # Save the destination image with the source's EXIF data
    destImg.save(destImgPath, exif=piexif.dump(exifData))

    # Copy file attributes for last accessed time and modified time
    srcImgStats = os.stat(srcImgPath)

    # set file ownership information (applicable only in unix systems)
    # os.chown(destImgPath, srcImgStats.st_uid, srcImgStats.st_gid)

    # set modified time and last accessed time
    os.utime(destImgPath, (srcImgStats.st_atime, srcImgStats.st_mtime))

def compressImage(srcImgPath, destImgPath, maxWidth, quality=100):
    # open source image
    image = Image.open(srcImgPath)

    # get the image dimensions
    width, height = image.size

    # Resize image if necessary
    if width > maxWidth:
        newHeight = height*(maxWidth/width)
        image.thumbnail((maxWidth, newHeight))

    # Save the new image
    outFname = destImgPath
    print(f"saving {outFname}")
    image.save(outFname, 'JPEG', quality=quality)

    # copy metadata from source image to destination image
    copyMetadata(srcImgPath, destImgPath)

# Example usage
inpFolder = r"D:\\pics"
outFolder = r"D:\\pics1"
maxWidth = 1280
qualityPerc = 100

for imgIter, imgPath in enumerate(glob.glob(inpFolder+r"\\*.jpg")):
    print(f"{imgIter} : processing {imgPath}")
    outFileName = pathlib.Path(imgPath).name
    outFilePath = os.path.join(outFolder, outFileName)
    compressImage(imgPath, outFilePath, maxWidth, qualityPerc)

print("process complete...")

```

## References
* Pillow documentation - https://pillow.readthedocs.io/en/latest/installation/basic-installation.html
* 
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTAzNjQ5ODk3MSw4MjQ1NjUxXX0=
-->