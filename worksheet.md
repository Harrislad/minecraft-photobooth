# Minecraft Photobooth

Create a Photobooth in Minecraft, which you the player enter the Photobooth it triggers the PiCamera and takes your picture, don't forget to smile.  Before starting ensure that your PiCamera is attached to the Raspberry Pi and enabled in the settings.  This is covered in this tutorial.  Once you have connected the camera boot up the Raspberry Pi

## Importing the Minecraft API and PiCamera Module

The first part of the program is to import the Minecraft API. (Application Programming Interface) This enables you to connect to Minecraft and use Python to code.  This will import the PiCamera module to control the camera and the time module to add a small delay between taking the photo and then taking the next photo.

1. Open the LX Terminal

2. Type `sudo IDLE`, this will load the Python IDLE code editor which you will use to write the Photobooth program

3. Open a new window

4. Enter the code shown below and save    
   
``` python
from mcpi import minecraft​
​mc = minecraft.Minecraft.create()
import time
import picamera
```

## Testing the PiCamera

Next we need to create a function which will control the PiCamera.  A function is made up of a number of lines of code which control a task, in this example they control the PiCamera.  However, it takes several lines of code to do this. By creating a function you can use a short word or phrase to call the lines of code.  In the code below it triggers the PiCamera every time the `take_the_pic()` function is called.   

1. Enter the code below

``` python
def take_the_pic():
	with picamera.PiCamera()as camera:
		camera.start_preview()
		time.sleep(2)
		camera.capture('selfie.jpg')

take_the_pic()		
``` 	

We have set the camera to show a two second preview so that you can strike your pose and smile before the picture is taken.  The image is stored as a file called, selfie.jpg

## Building a Photobooth 

Now we need to create a Photobooth in the Minecraft environment, this is done manually and can be built where ever you want to locate it.  To open Minecraft, 

1. Click the start button

2. Select games, coding and Minecraft.  

3. When it opens create a new world.

Using any block type, create a Photobooth, this can be any shape but should have at least one block width of free space inside so that the player can enter.

![](images/Photobooth.jpg)

Once you have created your Photobooth move your player inside and onto the trigger block.  This is the block that the player stands on to run the function that you wrote in step 1, it will trigger the PiCamera.  In the Minecraft environment your position is measured with the `x`, `y` and `z` axis.  Look at the top right of the window and you will see the `x`, `y`, `z` co-ordinates of your player, for example `10.5`, `9.0`, `-44.3`.  Assuming you are still in the Photobooth then these are also the `x`, `y`, `z` co-ordinates of the 'trigger' block in your Photobooth.
 
1. Walk into your Photobooth

2. Record the `x`, `y`, `z`, co-ordinates of your PiCamera 'trigger' block.

## Finding where I am?

When you are playing Minecraft your the program will need to check that you are inside the Photobooth, if you are then it will trigger the `take_the_pic` function and take a picture.  To do this Minecraft needs to know where you are in the world, read this and record your position.   To find your position you use the code, `x, y, x = mc.player.getPos()`.  This measures the `x`, `y`, `z` position of your player and saves the values.  You can then use `print pos.x` to print the `x` value.  Now you now the position of the player you can test to see if they are in the Photobooth. 

1. Add the function below to your PiCamera program

``` python
def where_am_i():
	while True:
		x, y, z, = mc.player.getPos()
```
	
## Testing that you are in the Photobooth 
 
At this point we have a Photobooth, the co-ordinates of the trigger block, and a function to control the PiCamera and take a picture.  The next step is to test the program identifies when you are in the Photobooth.  To do this we must create a loop which checks if your player's co-ordinates match the trigger block co-ordinates. If they do, then you are standing in the Photobooth.  To do this we use a simple `if` statement, we call these conditionals.  Add the code below to your program. 

```python
while True:
	where_am_i()
	time.sleep(2)
	if x >= 10.5 and y == 9.0 and z == -44.3:
		print ("You are at the Photobooth!")   

where_am_i()		
```

1. Save the program and press F5 to test it.

2. Walk into your Photobooth

You will note that the `if` statement checks if `x` value is greater than or equal to 10.5, this is ensure that it picks up the block as it could have a value of 10.6.  Remember to replace the `x`, `y` and `z` values with the values from your Photobooth.

## Putting it all together Part 1

Now you have a working Photobooth we need to add the PiCamera to take a picture.   We will replace the console message with a message in Minecraft to tell you that you are in the Photobooth, a quick reminder to smile and then call the PiCamera function, `take_the_pic()`.  Displaying a message is easily achieved by using the code `mc.postToChat("You are in the Photobooth!")`    
 
1. Comment out the print "You are at the Photobooth!"   

2. Under and in-line with the commented out `###You are at the Photobooth`, add the following code

```python
mc.postToChat("You are in the Photobooth!")
time.sleep(1)
mc.postToChat("Smile!")
time.sleep(1)
take_the_pic()
mc.postToChat("Check out your picture")
time.sleep(5)
```
3. Delete the `where_am_i()` line	

## Putting it all together Part 2

Well done you are nearly there, the final part of the project is to run the program and call the function to check where you are.  You will notice now that your original `where_am_I()` function includes all the code to check the players location and trigger the camera.  Add a simple chat message to prompt the player to find the Photobooth and you are ready.  

1. Add the code below to the bottom of your program

```python
mc.postToChat("Find the Photo-Booth")
where_am_i()
```
2. Save the program

3. Press F5 to run and test the Photobooth

## What next

1. Add a specific block which triggers the camera

2. Add further blocks to control PiCamera settings such as taking a video or applying a filter 

3. Use blocks to start and stop the PiCamera recording a video

