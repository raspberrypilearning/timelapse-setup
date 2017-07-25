## Reducing the file size

Currently, your animated GIF is probably sitting at around the 10MB range, which is a little large for a ten-frame animation. This is because your Pi camera captures images at a resolution of 3280 x 2464 if you have a Camera Module v2, or 1920 x 1080 if you have an original Camera Module. You can produce smaller GIFs by using a smaller image resolution.

- Go back to your `timelapse.py` file. Now add in a single new line to set the resolution of the images:

	``` python
	from picamera import PiCamera
	from os import system
	
	camera = PiCamera()
	camera.resolution = (1024, 768)
	
	for i in range(10):
		camera.capture('image{0:04d}.jpg'.format(i))
		
	system('convert -delay 10 -loop 0 image*.jpg animation.gif')
	```
	
- If you want even smaller GIFs, then choose an even smaller resolution.

