---
title: Image Manipulation with Python Pillow
markup: mmark
date: 2019-10-27
bigimg: [{src: "/img/2019-10-27-python-pillow.jpg", desc: "Saint-Tropez (July 2018)"}]
tags: ["python", "code", "website"]
---

Normally I use [GIMP](https://www.gimp.org/) when I need to resize, crop or retouch images in various ways. However, for my last [post](/post/2019-10-19-first-post/) on the Berlin Festival of Light I would have had to manually resize and crop a whole bunch of images at a time. That's why I took a look how Python could help with this task, and found PIL, the Python Imaging Library, in newer versions known as [Pillow](https://python-pillow.org/).

<!--more-->

I decided to write a small Python script, without any sophisticated bells and whistles, just good enough to get the task done. It is supposed to cover the following workflow:
* Implicity assume `.jpg` files with aspect ratio 16:9, because that's currently my default setting for my Lumix camera.
* Loop through the images in an input directory
* Let function `scale_image()` resize an image to 1920x1080 pixels, then save it in the output directory
* Let function `crop_image()` produce six different thumbnails out of the rescaled image, in order to give some choice, and save them in the output directory
* Finally, I inspect the thumbnails with IrfanView and manually delete the redundant ones.

Here's the code:


{{< highlight python "linenos=inline">}}
from PIL import Image
import os
 
def scale_image(input_image_path, scaled_image_path): 
    """ Resize an image to 1920 pixels width and save it into out directory"""
    original_image = Image.open(input_image_path) 
    original_image.thumbnail((1920, 10000), Image.ANTIALIAS)
    original_image.save(scaled_image_path)
 

def crop_image(scaled_image_path):
    """ 
    Produce all-in-all 6 thumbnails of an image: 2 centered, in different sizes, 
    and then 4 other ones off-center, in order to present options to choose the 
    nicest version. All thumbs are resized to 500x500 pixels
    """
    scaled_image = Image.open(scaled_image_path)
    f, e = os.path.splitext(scaled_image_path)
    
    cropdims = [(510,  90, 1410, 990),
                (610, 190, 1310, 890),
                (510,  90, 1210, 790),
                (510, 290, 1210, 990),
                (710,  90, 1410, 790),
                (710, 290, 1410, 990)]
    
    length = len(cropdims)

    for i in range(length):    
        thumb = scaled_image.crop(cropdims[i])
        thumb_image_path = f + '-thumb' + str(i) + e
        thumb.thumbnail((500, 10000), Image.ANTIALIAS)
        thumb.save(thumb_image_path)
 

if __name__ == '__main__':
    in_path = "C:/Users/JOACWEIS/Pictures/input/" 
    out_path = "C:/Users/JOACWEIS/Pictures/output/" 
    input_path = os.listdir(in_path)
    output_path = os.listdir(out_path)
    
    for item in input_path:
        input_image_path = in_path + item
        if os.path.isfile(input_image_path):
            f, e = os.path.splitext(out_path + item)
            scaled_image_path = out_path + item
            scale_image(input_image_path, scaled_image_path)
            crop_image(scaled_image_path)
{{</ highlight >}}


Using Pillow is straightforward, the [documentation](https://pillow.readthedocs.io/en/stable/) is  extensive and gives lots of examples. A crucial class in the Python Imaging Library is the `Image` class. It is defined in the `Image` module and provides a PIL image on which manipulation operations can be carried out. An instance of this class can be created in several ways: by loading images from a file, creating images from scratch or as a result of processing other images. After obtaining an `Image` object, we can use the methods and attributes defined by the class to process and manipulate it.

I found it desirable to thumbnail all images so that they have the same width and height. Using the `crop()` function, 6 quadratic thumbs are created, a centered large one, as well as 5 smaller ones, one of them centered, the others slight offset along the x and y axes. Resizing to 500x500 pixels is done using the Pillow  `thumbnail()` method. It takes a tuple (width,  height), and the image will be resized so that the width and height of the image are equal or smaller than the specified shape, retaining the aspect ratio of the image. I could also have used the `resize()` function, which also accepts a size tuple, but then resizes the image to fit within the specified size, potentially distorting the picture.
