# create-video-from-images

For ubuntu server

ติดตั้ง Package:
 - ImageMagick
 - ffmpeg

## ffmpeg

sudo apt-add-repository ppa:mc3man/trusty-media<br>
sudo apt-get update<br>
sudo apt-get install ffmpeg gstreamer0.10-ffmpeg

## ImageMagick
sudo apt-get install imagemagick<br>
sudo apt-get install php5-imagick

Resizing Images from the Command Line
ImageMagick includes "mogrify" which is a fine tool for easily changing image size and resolution. Great for converting images for uploading to the web, or preparing large images for video. For example, the following code re-sizes all *.JPG images to a maximum width of 800 pixels and a maximum height of 600 pixels. This will over-write the originals, so take copies of your snaps first!

mogrify -resize 800x600 *.JPG

Morphing Images Together
This step is only needed if you want to create a smooth transition between the images.

Another fine part of ImageMagick is the ability to morph images together. In the following example we take all *.JPG files and create 10 images for each "gap" between the images. The resulting set of images are saved as XXXXX.morph.jpg, where X is the next number in the series.

convert *.JPG -delay 10 -morph 10 %05d.morph.jpg

Creating a Video from Images
ffmpeg can be used to stitch several images together into a video. There are many options, but the following example should be enough to get started. It takes all images that have filenames of XXXXX.morph.jpg, where X is numerical, and creates a video called "output.mp4". The qscale option specifies the picture quality (1 is the highest, and 32 is the lowest), and the "-r" option is used to specify the number of frames per second.

ffmpeg -start_number 0 -i %05d.morph.jpg output.mp4
