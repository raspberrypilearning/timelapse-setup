## Taking a picture

You can start by writing a simple script to take a picture using the Camera Module.

- Open Thonny (`Menu` > `Programming` > `Thonny`.

- Create a new file (`File` > `New File`) and then save it as **timelapse.py**.

- Now with three simple lines of code, you can use Python to take a photo:

	``` python
	from picamzero import Camera

	camera = Camera()

	camera.take_photo('image.jpg')
	```

- Save (`Ctrl+s`) your script, and then run it by pressing `F5` on your keyboard.

- Open up your File Manager by clicking on the ![File Manager](images/file_icon.png) icon in the top-left of the screen, and double-click on `image.jpg`:

  ![selfie](images/selfie.jpg)
  
