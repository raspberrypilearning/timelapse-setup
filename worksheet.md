# Time-lapse animations with a Raspberry Pi

Time-Lapse photography uses multiple images taken over a length period of time, that are then stitched together to produce an animated sequence of images.

If you've never seen a time lapse before, then the one below is an example of what can be achieved.

![mung bean time-lapse](images/mungbeans.gif)

If you've never before used the Raspberry Pi Camera before, then it is probably a good idea to have a quick look through the first few steps in the [Getting Started with PiCamera](https://www.raspberrypi.org/learning/getting-started-with-picamera/worksheet/) resource, to familiarise your self with the device, and make sure it is working properly.

## Taking a picture

You can start by writing a simple script to take a picture using the Pi Camera.

1. Open IDLE (`Menu` > `Programming` > `Python 3 (IDLE)`

1. Create a new file. (`File` > `New File`) and then save it as **timelapse.py**.

1. Now with three simple lines of code, you can use Python to take a photo.

``` python
from picamera import PiCamera

camera = PiCamera()

camera.capture('image.jpg')
```

1. Save your script again, and then run it by pressing `F5` on your keyboard.

1. Open up your File Manager by clicking on the ![File Manager](images/file_icon.jpg) icon in the top left of the screen.

  ![selfie](images/selfie.jpg)
  
## Taking multiple images

You can take multiple images using the Pi Camera by capturing images using a loop. A `for` loop can be used to capture a set number of images.

1. Modify your file to incorporate a `for` loop. In this example, the Pi Camera will capture 10 images.

	``` python
	from picamera import PiCamera

	camera = PiCamera()

	for i in range(10):
		camera.capture('image.jpg')
	```
1. Save (`Ctrl+s`) and run (`F5`) your program. Then have a look inside your **File Manager** to see what has been created.

1. Can you see the problem? There is only one image there, and it's the last image that was taken. This is because, each image had the same file name, so was *over written* by the next image to be taken. This can be solved with a little modification of the script.

	``` python
	from picamera import PiCamera

	camera = PiCamera()

	for i in range(10):
		camera.capture('image{0:04d}.jpg'.format(i))
	```

1. If you look in the **File Manager** now, you should see 10 images named `image0000.jpg` up to `image0009.jpg`

1. The syntax `'image{0:04d}.jpg'.format(i)` adds the value of `i` which starts at `0` and ends at `9` to the file name. It also pads the number with zeros, so that there are always 4 digits. This will be important later on.

## Making a gif

Now that you know hoe to take multiple photos, let's see how you can turn that sequence into an animated gif. For this you're going to need the program **Imagemagick**. If you haven't already installed it there are instructions in the [software setup guide](software.md)

1. **Imagemagick** is a command line program that can be used to manipulate images. You can try it out, first of all, by opening up your terminal (`ctrl+alt+t`) and typing the following:

	``` bash
	convert -delay 10 -loop 0 image*.jpg animation.gif
	```

1. The `-delay` option sets the amount of time (in 100ths of a second) between frames. The `-loop` option sets the number of times the gif will loop. Here the `0` tells it to loop for ever.

1. This will take a little time to run, but once it's complete you should see the file `animation.gif` in the **File Manager**

![animated](images/animation.gif)

1. You can double click this and watch the animation in **Image Viewer**. Again, give it a little time to open as it's probably a fairly large file.

1. As with all command line programs, you can call **Imagemagick** from within python. You just need to use the `os` library, as shown below.

    ``` python
	from picamera import PiCamera
	from os import system
	
	camera = PiCamera()

	for i in range(10):
		camera.capture('image{0:04d}.jpg'.format(i))
		
	system('convert -delay 10 -loop 0 image*.jpg animation.gif')
	print('done')
    ```

1. This will take a little time to run. You should see the word `done` printed in the *Shell* when the script has finished. Your new `animation.gif` will be playable from the **File Manager** after a couple of minutes.

## Reducing the file size.

Currently your animated gif is probably sitting at around the 10MB range, which is a little large for only a 10 frame animation. This is because your Pi Camera captures images at a resolution of 3280 x 2464 if you have a Pi Camera 2 or 1920 x 1080 if you have a Pi Camera 1. You produce smaller gifs by using a smaller image resolution.

1. Go back to your `timelapse.py` file. Now add in a single new line to set the resolution of the images.

    ``` python
	from picamera import PiCamera
	from os import system
	
	camera = PiCamera()
	camera.resolution = (1024, 768)
	
	for i in range(10):
		camera.capture('image{0:04d}.jpg'.format(i))
		
	system('convert -delay 10 -loop 0 image*.jpg animation.gif')
    ```
	
1. If you want even smaller gifs, then choose an even smaller resolution.

## Adding a delay

The point of time-lapse is to take pictures every few minutes or even hours. To do this you can pause your program between captures, using the `time` library.

1. Back in your `timelapse.py` file, alter the code so that you can import the `sleep` function, and then pause the script after each `capture`

    ``` python
	from picamera import PiCamera
	from os import system
	from time import sleep
	
	camera = PiCamera()
	camera.resolution = (1024, 768)
	
	for i in range(10):
		camera.capture('image{0:04d}.jpg'.format(i))
		sleep(60)
		
	system('convert -delay 10 -loop 0 image*.jpg animation.gif')
    ```

1. In the above example a picture is taken once every 60 seconds, and 10 pictures are taken in total. You can now modify the values for the `range()` and `sleep()` functions to whatever suits your purpose. For capturing a flower opening, then a picture a minute for a couple of hours would suffice. If you wanted to do a time-lapse of a fruit rotting, then two or three pictures a day might be more appropriate.

1. Set up your Raspberry Pi with the Pi Camera pointing at your target, run the script and then sit back and wait for the gif to be created.

## What Next?
- Now that you've managed to do some time-lapse photography, why not have a go at some other PiCamera resources like:
    - [Minecraft Photo-booth](https://www.raspberrypi.org/learning/minecraft-photobooth/)
	- [Push Button Stop Motion](https://www.raspberrypi.org/learning/push-button-stop-motion/)
	- [Infrared Bird Box](https://www.raspberrypi.org/learning/infrared-bird-box/)
- You could even have a go at playing around with some slow motion video captures.
