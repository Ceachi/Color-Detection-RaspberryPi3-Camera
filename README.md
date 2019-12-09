# Color Detection using RaspberryPi3

Components:
1. [RaspberryPi3](https://www.optimusdigital.ro/ro/placi-raspberry-pi/5091-raspberry-pi-3-model-b-plus.html?gclid=Cj0KCQiA_rfvBRCPARIsANlV66NjQ5PKwVEPBRB92iI6XPAWiCcLWImjVmlzxI3xYKhCtg-SR_kj6K8aAua8EALw_wcB)  or [RaspberryPi4](https://www.googleadservices.com/pagead/aclk?sa=L&ai=DChcSEwi_8OX1pajmAhVVqpoKHeKbCZEYABAHGgJsbQ&ohost=www.google.ro&cid=CAESQOD2M75QMIAaIlTi-WE_IxqCnFv8DnTYq_-TSn1KPr-pX_2jinaFwaYLR65xp6SdruLTQ8XQNu25zGfltbCN3c4&sig=AOD64_06JXml0MatRhcIe1BY_NO132qulw&q=&ved=2ahUKEwiW2dz1pajmAhUaAxAIHXTrCAIQ0Qx6BAgOEAE&adurl=):
2. [Cameră Raspberry Pi V2](https://cleste.ro/camera-raspberry-pi-v2.html)
3. [Camera cable 30cm](https://www.optimusdigital.ro/ro/camere/1352-camera-module-v2.html?gclid=Cj0KCQiA_rfvBRCPARIsANlV66M0R9YHRWtbHxZSUk8LLrREZshoa1mj4fY_iAEA_wM0ZHq7Rggle40aAsXoEALw_wcB)

# Informations about the camera  
1.Connect the camera to Raspberry.
The connection of the camera is done through a serial interface dedicated to the camera. To locate this interface, see the attached image below.  
CAREFUL!!! Connect the module when the development board is stopped.  
![alt text](http://url/to/img.png)  
2. Activate the camera.
Camera activation is done by opening the menu and selecting  Preferences> Raspberry Pi Configuration Tool.   Once you have opened the configuration tool, select the INTERFACES  tab  and check the ENABLED box   next to the camera. Restart the Raspberry board and proceed to the next step. 
Once you've connected your camera to the Raspberry Pi, an easy way to check if everything is working properly is to write a simple code in Python. 
Open the Python 3 pre-installed development environment  (IDLE). Create a new file and rename it as you wish (you cannot name it  picamera.py  ). 
Enter the following code:
```py
"    from  picamera  import  PiCamera
```
10411000001267 from  time  import  sleep

    camera = Camera ()
    camera.start_preview ()
    sleep ( 10 )
    camera.stop_preview () " 

Now save the file with the CTRL + S  command  and execute it by pressing  F5.  The code above is meant to show what the camera sees for 10 seconds. Set the orientation with the command " camera.rotation = X" , where  X  can have the value 0, 90, 180 or 270.

4. Taking a photo:

A photo is taken by the command " camera.capture ('X  ' )" , and  X  represents the location where you want to save the photo. You use this command according to the SLEEP statement  (10)  in the code attached above. It is recommended that  SLEEP  be at least 2 to give the module enough time to automatically adjust the brightness level.

It is also possible to take several pictures one at a time, using the FOR statement  . The code attached below takes 5 pictures one after the other, at an interval of 5 seconds. These will be saved in "/ home / pi / Desktop /".

```py
"camera.start_preview ()
   for  i  in  range ( 5 ):
   sleep ( 5 )
   camera.capture ( ' /home/pi/Desktop/image%s.jpg '  % s)
   camera.stop_preview () "
```
CAREFUL!  Be sure to specify the format in which the photo is saved, for example. JPG.



5. Making a video.

Recording a video is very much like taking a photo. Instead of using the command "camera.capture", we will use the command " camera.start_recording ('DESTINATION')" .

The code attached below records video for 10 seconds.
```py
 "camera.start_preview ()

    camera.start_recording ( ' /home/pi/video.h264 ' )

    sleep ( 10)

    camera.stop_recording ()

    camera.stop_preview () "
```

CAREFUL!  Remember to specify the format in which the video is saved, for example. H264  .

6.Configure the camera and use special effects.

Resolution setting:  "  camera.resolution (X, Y)"  , where  X  and  Y  represent the resolution used. For photos, the maximum resolution is 2592 x 1944, and for video it is 1920 x 1080. Also, the minimum resolution is 64 x 64.
Setting the number of frames per second:  "camera.framerate = X",  where  X  represents the number of frames per second.
Add text over images:  "camera.annotate_text = X" , where  X  represents the text you want over images. Also, the text size can be changed through the command  "camera.annotate_text_size = Y"  , where  Y  can have a value between 6 and 160.
Brightness setting:  "camera.brightness = X"  , where  X  can have a value between 0 and 100.
Contrast setting: " camera.contrast = X" , where  X  can have a value between 0 and 100.
Using a special effect: " camera.image_effect = 'X'" , where  X  is the name of a special effect:
none,  negative,  solarize,  sketch,  denoise,  emboss,  oilpaint,  hatch,  gpen,  pastel,  watercolor,  film,  blur,  saturation,  colorswap,  washedout,  posterise,  colorpoint,  colorbalance,  cartoon,  deinterlace1 And deinterlace2
Setting a white balance mode:  "camera.awb_mode = 'X'" , where X is the name of a mode:
off,  auto,  sunlight,  cloudy,  shade,  tungsten,  fluorescent,  incandescent,  flash And horizon
Setting an Exposure Mode:
off,  auto,  night,  nightpreview,  backlight,  spotlight,  sports, snow,  beach,  verylong,  fixedfps,  antishake, And fireworks



# Color Detection for Red, Green, Blue, Yellow
First make sure you create an empty folder, in your current directory: "./finishImages"

**test_camera_final.py** -> this is the final script code, after you are making the calibration. This will return your detecting color
**test_camera.py** -> this is used for calibration, run this first, then **calibrate_camera.py**
**calibrate_camera.py** -> this will be used to calibrate the Max and Min values for your calibration (The HSV for every color you are trying to identify)
![alt text](http://url/to/img.png)


**Step1**  

run the following script:  
```py
sudo python3 test_camera_final.py
```
if you are not happy with the results, go to Step2 to make your own calibrations  

**Step2**

* open test_camera.py
* You only need to modify the Maximum and minimum HSV values from this matrix:
```py
        boundariesHSV = [
            ([170, 109, 75], [180, 255, 255]),  # red
            ([97, 55, 75], [125, 255, 255]),  # blue
            ([4, 109, 75], [22, 255, 255]),  # yellow
            ([78, 20, 40], [104, 255, 255])  # green
        ]

```
Tips: only modify the 3 values from the minimum array, and the first value of the maximum array.  
For example ([170, 109, 75], [180, 255, 255]),  # red, I will change only the values 170,109,75 and 180

* How to find the right values? 
* first run: 
```py
sudo python3 test_camera.py
```
this will make a photo inside the folder *'./finishImages/*  
* now run:
```py
sudo python3 calibrate_camera.py
```
You will get the values like in this picture:  
![alt text](http://url/to/img.png)

- now get the values only on the minimum values on the array with label "1" and only the first element of the maximum array with the label "3", and put the new values inside the boundariesHSV[]. Rembemer, for the "1" array, get only the minimum values as possible, as well the maximum value of the first element in label"3" array

After that, test_camera.py again, until you find all the right values for each of RGBY arrays. And test it again.
In the end, paste boundariesHSV[] array values in the boundariesHSV[] array of test_camera_final.py.





