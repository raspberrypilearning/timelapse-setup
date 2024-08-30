## Taking multiple images

You can take multiple images using the Camera Module by capturing images with a loop. A `for` loop can be used to capture a set number of images.

- Modify your file to incorporate a `for` loop. In this example, the Pi Camera will capture 10 images:

	``` python
	from picamera import PiCamera

	camera = PiCamera()

	for i in range(10):
		camera.take_photo('image.jpg')
	```
- Save your script again and run (`F5`) your program. Then have a look inside your **File Manager** to see what has been created.

- Can you see the problem? There's only one image there, and it's the last image that was taken. This is because each image had the same file name, so it was overwritten by the next image to be taken. This is a problem which can be solved by a little modification of the script:

	``` python
	from picamzero import Camera

	camera = Camera()

	for i in range(10):
		camera.take_photo('image{0:04d}.jpg'.format(i))
	```

- If you look in the **File Manager** now, you should see ten images named `image0000.jpg` up to `image0009.jpg`.

- The syntax `'image{0:04d}.jpg'.format(i)` adds the value of `i`, which starts at `0` and ends at `9`, to the file name. It also pads the number with zeros, so that there are always 4 digits. This will be important later on.

