# PnR-Final
The old final project for [Gilmour Academy's](http://www.gilmour.org) Programming and Robotics class. Your job is to design a self-driving script that will safely move your GoPiGo from one side of an obstacle course to another, without hitting an object or turning around and heading the wrong way.
 
The ideal solution will work quickly and will output detailed description of the robot's thinking to the SSH console. 

## What I've tried 



## Useful Info

All of your work will go into the **student.py** file. Your **student.py** file has `class GoPiggy` which inherits all the properties from the teacher's `class Pigo`. The parent class, Pigo, is in the **pigo.py** file. Leave that file alone. All your work is done in the **student.py** file. 
_Why shouldn't I modify the **pigo.py** file?_
As our project progresses, I will be updating the **pigo.py** file with helpful new methods. If you put all your work into the **student.py** file, you won't lose anything when you update **pigo.py**. And remember: your `class GoPiggy` is the child, so it overrides the `class Pigo`. So copy and paste a method from **pigo.py** to your **student.py** and make your improvements there. 


### Custom Methods Students Can Use
[The GoPiGo API](http://www.dexterindustries.com/GoPiGo/programming/python-programming-for-the-raspberry-pi-gopigo/) is how we speak to our robot. It's why we have `from gopigo import *` at the top of our code. You **must become familiar with the API's commands**. 
Below are some some helpful methods. These will not be enough for you to complete your project, but I hope they will help you get started. These Pigo methods use the GoPiGo API. 

`self.is_clear()`
Will perform a three point check around self.MIDPOINT and will return True if no distance is shorter than the stop dist.

`self.choose_path()`
Performs self.flushScan() and then self.wideScan() to scan the area in front. The method averages the distances and returns a string "right" or "left" depending on the average distance around the MIDPOINT.

`self.encR(x)`, `self.encL(x)`, `self.encF(x)`, `self.encB(x)`
Will set the encode value passed to the method and executes the rotate, fwd, or bwd

`self.wide_scan()`
This will fill your self.scan array with distances self.MIDPOINT-60, self.MIDPOINT+60, +2

`self.flush_scan()`
Resets the list that stores the distances of the ultrasonic sensor. 

`self.status()`
Prints your current power level, motor speeds, midpoint and stop distance. If one of your ideas isn't working the way you want it to, you can add a couple status updates in your code to help you see what's happening with your robot.

`self.stop()`
A more reliable stop command. It repeats the GoPiGo's stop() method three times to assure that the command is not lost. 

`self.calibrate()`
This method is built into the `class GoPiggy`'s initilization. When you first start your app, it will ask you to calibrate the midpoint and the motor speeds. *Note: The values that you receive in this method will not be saved unless you update the variables at the top of your code* 

###Want some ideas?
* I'll start you guys off by showing you how to use `self.encF(5)` while `self.isClear()` returns True. And when that loop exits, we'll use `self.choosePath()` to tell us whether we should `encR(5)` or `encL(5)`. But this is a slow and error-prone approach. 
* You can develop your own `def cruise(self):` method that will replace the while loop described above. Instead of inching forward, you could check the distance in front of you while driving forward. Start by making your robot look straight forward then start moving with `fwd()`. Enter a while True loop that checks `us_dist(15)`. If it sees something closer than your stop distance, break out of the loop and `self.stop()`. Otherwise, wait a 0.05 seconds before the loop restarts. 
* Is your robot turning the wrong way a lot? You could create a new *instance variable* that keeps track of how much you've turned. You could start this variable out at 0, which represents the correct direction. If your robot uses `self.encL(x)` you add whatever `x` is to your turn variable. If you use `self.encR(x)` you could then subtract `x` from your turn variable. Then, when your robot is deciding which way to turn, you could program the robot to prefer the turn that will bring this variable closer to 0. 
