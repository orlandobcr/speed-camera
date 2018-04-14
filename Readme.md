# SPEED CAMERA - Object Motion Tracker [![Mentioned in Awesome <INSERT LIST NAME>](https://awesome.re/mentioned-badge.svg)](https://github.com/thibmaek/awesome-raspberry-pi)
### RPI, Unix and Windows Speed Camera Using python, openCV, USB Cam or RPI camera module
## For Details See [Program Features](https://github.com/pageauc/speed-camera/wiki/Program-Description#program-features) and [Wiki Instructions](https://github.com/pageauc/speed-camera/wiki) and [YouTube Videos](https://github.com/pageauc/speed-camera#links)

## RPI Quick Install or Upgrade   
***IMPORTANT*** - A raspbian **sudo apt-get update** and **sudo apt-get upgrade** will
**NOT** be performed as part of   
**speed-install.sh** so it is recommended you run these prior to install
to ensure your system is up-to-date.     

***Step 1*** With mouse left button highlight curl command in code box below. Right click mouse in **highlighted** area and Copy.     
***Step 2*** On RPI putty SSH or terminal session right click, select paste then Enter to download and run script.  

    curl -L https://raw.github.com/pageauc/speed-camera/master/speed-install.sh | bash

This will download and run the **speed-install.sh** script. If running under python3 you will need opencv3 installed.
See my Github [menu driven compile opencv3 from source project](https://github.com/pageauc/opencv3-setup)

## Program Description   
This is a raspberry pi, Windows, Unix Distro computer openCV object speed camera demo program.
It is written in python and uses openCV to detect and track object motion.
This can be vehicles or any other moving objects.  It tracks the speed of
the largest moving object in the camera view above a minimum pixel area.
The results are recorded on speed photos and in a CSV data file that can be
imported to a spreadsheet or other program for additional processing. You
can also run ***makehtml.py*** to generate html files that combine csv and image
data. (Does not work with ***secpicam480.py*** and ***secwebcam480.py*** plugins.

The program will detect motion in the field of view and use opencv to calculate
the largest contour and return its x,y coordinate. User variables are stored in the ***config.py** file.
Motion detection is restricted between ***y_upper*** and ***y_lower*** variables (road or area of interest).
If a track is longer than ***track_len_trig*** variable then average speed will be 
calculated (based on ***cal_obj_px*** and ***cal_obj_mm*** variables) and a speed photo will be
taken and saved in ***media/images*** dated subfolders per variable ***imageSubDirMaxFiles*** = ***1000*** 
(see config.py). If ***log_data_to_CSV*** = ***True*** then a
***speed-cam.csv*** file will be created/updated with event data stored in
CSV (Comma Separated Values) format. This can be imported into a spreadsheet, database, Etc for further processing.
  
## Requirements
Requires a [***Raspberry Pi computer***](https://www.raspberrypi.org/documentation/setup/) and a [***RPI camera module installed***](https://www.raspberrypi.org/documentation/usage/camera/)
or USB Camera plugged in. Make sure hardware is tested and works. Most [RPI models](https://www.raspberrypi.org/products/) will work OK. 
A quad core RPI will greatly improve performance due to threading. A recent version of 
[Raspbian operating system](https://www.raspberrypi.org/downloads/raspbian/) is Recommended.   
or  
A ***MS Windows or Unix distro*** computer with a USB Web Camera plugged in and a
[recent version of python installed](https://www.python.org/downloads/)
For Details See [Wiki](https://github.com/pageauc/speed-camera/wiki/Prerequisites-and-Install#windows-or-non-rpi-unix-installs).

# Note
I am looking at revamping logic for using speed camera as a security camera. Currently the
plugins ***secpicam480.py*** and ***secwebcam480.py*** do not work very well since only horizontal x
changes are tracked.  I will add xy triangulation tracking with no speed as well as support
for IP cameras. ***SECURITY_CAM_MODE*** will not support ***makehtml.py*** or csv logging. These changes
 will take some time so be patient.  Claude 

***IMPORTANT*** speed-cam.py ver 8.x Requires Updated config.py and plugins.

    cd ~/speed-camera
    cp config.py config.py.bak
    cp config.py.new config.py
    
To replace plugins rename (or delete) plugins folder per below

    cd ~/speed-camera
    mv plugins pluginsold   # renames plugins folder
    rm -r plugins           # deletes plugins folder

Then run menubox.sh UPGRADE menu pick.
 
## Manual Install or Upgrade   
From logged in RPI SSH session or console terminal perform the following. Allows you to review install code before running

    cd ~
    wget https://raw.github.com/pageauc/speed-camera/master/speed-install.sh
    more speed-install.sh       # You can review code if you wish
    chmod +x speed-install.sh
    ./speed-install.sh  # runs install script.
    
## Run to view verbose logging 

    cd ~/speed-camera    
    ./speed-cam.py
    
## Run menubox.sh 

    cd ~/speed-camera
    ./menubox.sh

Admin speed-cam Easier using menubox.sh (Once calibrated and/or testing complete)  
![menubox main menu](https://github.com/pageauc/speed-camera/blob/master/menubox.png)     

## Links
* YouTube Speed Lapse Video https://youtu.be/-xdB_x_CbC8
* YouTube Speed Camera Video https://youtu.be/eRi50BbJUro
* YouTube motion-track video https://youtu.be/09JS7twPBsQ
* Speed Camera RPI Forum post https://www.raspberrypi.org/forums/viewtopic.php?p=1004150#p1004150
* YouTube Channel https://www.youtube.com/user/pageaucp 
* Speed Camera GitHub Repo https://github.com/pageauc/speed-camera     
    
## Windows or Non RPI Unix Installs
For Windows or Unix computer platforms (non RPI or Debian) ensure you have the most
up-to-date python version.  For Downloads visit https://www.python.org/downloads    

The latest python versions include numpy and recent opencv that is required to run this code. 
You will also need a USB web cam installed and working. 
To install this program access the GitHub project page at https://github.com/pageauc/speed-camera
Select the ***green Clone or download*** button. The files will be cloned or zipped
to a speed-camera folder. You can run the code from from ***python IDLE application (recommended)***, GUI desktop
or command prompt terminal window.        
    
### IMPORTANT
Speed Camera will start in ***Calibration Mode***    
Review settings in config.py file and edit variables with nano as required.
You will need to perform a calibration to set the correct value for ***cal_obj_px*** and ***cal_obj_mm*** 
variables based on the distance from camera to objects being measured for speed.  
See [Calibration Procedure](https://github.com/pageauc/speed-camera#calibration-procedure) below for more details.     
    
See [How to Run](https://github.com/pageauc/speed-camera#how-to-run) speed-cam.py section below

## Credits  
Some of this code is based on a YouTube tutorial by
Kyle Hounslow using C here https://www.youtube.com/watch?v=X6rPdRZzgjg

Thanks to Adrian Rosebrock jrosebr1 at http://www.pyimagesearch.com 
for the PiVideoStream Class code available on github at
https://github.com/jrosebr1/imutils/blob/master/imutils/video/pivideostream.py
  
Have Fun   
Claude Pageau    
YouTube Channel https://www.youtube.com/user/pageaucp   
GitHub Repo https://github.com/pageauc
