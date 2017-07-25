## Adding a delay

The point of time-lapse is to take pictures every few minutes or even hours. To do this you can pause your program between captures, using the `time` library.

- Back in your `timelapse.py` file, alter the code so that you can import the `sleep` function, and then pause the script after each `capture`:

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

- In the above example a picture is taken once every 60 seconds, and ten pictures are taken in total. You can now modify the values for the `range()` and `sleep()` functions to whatever suits your purpose. If you want to capture a flower opening, then a picture a minute for a couple of hours would suffice. If you were making a time-lapse of a fruit rotting, then two or three pictures a day might be more appropriate.

- Set up your Raspberry Pi with the Camera Module pointing at your target, run the script, and then sit back and wait for the GIF to be created.

