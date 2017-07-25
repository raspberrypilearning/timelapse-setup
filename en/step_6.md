## Making a GIF

Now that you know how to take multiple photos, let's see how you can turn that sequence into an animated GIF. For this you're going to need the program **ImageMagick**. If you haven't already installed it, there are instructions in the [software setup guide](software.md).

- ImageMagick is a command line program that can be used to manipulate images. First of all, you can try it out by opening up your terminal (`Ctrl+Alt+t`) and typing the following:

	``` bash
	convert -delay 10 -loop 0 image*.jpg animation.gif
	```

- The `-delay` option sets the amount of time (in 100ths of a second) between frames. The `-loop` option sets the number of times the GIF will loop. Here the `0` tells it to loop forever.

- This will take a little time to run, but once it's complete you should see the file `animation.gif` in the File Manager:

	![animated](images/animation.gif)

- You can double-click this and watch the animation in Image Viewer. Again, give it a little time to open as it's probably a fairly large file.

- As with all command line programs, you can call ImageMagick from within Python. You just need to use the `os` library, as shown below:

	``` python
	from picamera import PiCamera
	from os import system
	
	camera = PiCamera()

	for i in range(10):
		camera.capture('image{0:04d}.jpg'.format(i))
		
	system('convert -delay 10 -loop 0 image*.jpg animation.gif')
	print('done')
	```

- This will take a little time to run. You should see the word `done` printed in the shell when the script has finished. Your new `animation.gif` will be playable from the File Manager after a couple of minutes.

