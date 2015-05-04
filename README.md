# PiSentinel

**PiSentinel** is a Raspberry Pi specific fork of Sentinel (https://github.com/AlexNisnevich/sentinel), a USB missile launcher face-tracking solution. It will attempt to track faces, continually point the missile launcher at the clearest face, and optionally shoot foam missiles.

Impress your friends! Intimidate your enemies!

1\.  [How it Works](#howitworks)  
1.1\.  [Video Demonstration](#videodemonstration)  
2\.  [Hardware Requirements](#hardwarerequirements)  
3\.  [Software Requirements and Installation](#softwarerequirementsandinstallation)  
3.1\.  [Linux](#linux)  
3.2\.  [Windows](#windows)  
3.3\.  [Mac OS X](#macosx)  
4\.  [Usage](#usage)  

<a name="howitworks"></a>

## 1\. How it Works

Alex Nisnevich wrote [an article](http://alex.nisnevich.com/blog/2013/02/19/face_tracking_with_open_cv_and_a_usb_missile_launcher.html) about how the original Sentinel was implemented using OpenCV.

<a name="videodemonstration"></a>

### 1.1\. Video Demonstration

Here's a quick video of the original Sentinel.

[![Link to Youtube video](images/youtube/L2It-kK0yfM.png)](http://www.youtube.com/watch?v=L2It-kK0yfM)

<a name="hardwarerequirements"></a>

## 2\. Hardware Requirements
- **[Dream Cheeky brand USB missile launcher](http://www.amazon.com/Dream-Cheeky-908-Electronic-Reference/dp/B004SAYO46)** (tested with the Thunder model, should also work with the Storm model)
- [Raspberry Pi] (https://www.raspberrypi.org) running linux (the code was developed and tested on a Raspberry Pi B running Raspbian)
- [Raspberry Pi camera module] (https://www.raspberrypi.org/products/camera-module/)

<a name="softwarerequirementsandinstallation"></a>

## 3\. Software Requirements and Installation

If you're running on Raspbian 3.18+, you can simply run the included installation script:
```
> sudo install/ubuntu_debian.sh
```

Otherwise (or if the script doesn't work for you), install the following dependencies:

- **Python** 2.7, 32-bit
- **libusb** 1.0 (in Raspbian, `sudo apt-get install libusb-dev`)
- **PyUSB** 1.0 (https://github.com/walac/pyusb)
- **OpenCV** 2.3+ with Python bindings
  - In Raspbian, `sudo apt-get install python-opencv` will install the correct version
  - Alternatively, you can follow [these instructions](http://www.pyimagesearch.com/2015/02/23/install-opencv-and-python-on-your-raspberry-pi-2-and-b/)
- **streamer** (in Raspbian, `sudo apt-get install streamer`)
- **ImageMagick** (in Raspbian, `sudo apt-get install imagemagick`)
- **picamera** (http://picamera.readthedocs.org/en/release-1.9/index.html)

After installing all of the software requirements, you can run PiSentinel:
```
> sudo ./pisentinel.py
```

Alternatively, if you do not want to run PiSentinel as root, you can set a udev rule for the USB missle launcher to allow other users to have access to the launcher. To do this add a rules file to `/etc/udev/rules.d` with the following line
```
SUBSYSTEM=="usb", ATTRS{idVendor}=="2123", ATTRS{idProduct}=="1010", MODE="0666", GROUP="plugdev"
```
and replace `ATTRS{idVendor}` and `ATTRS{idProduct}` with the correct values from `lsusb`.
<a name="usage"></a>

## 4\. Usage

```
Usage: sentinel.py [options]

Options:
  -h, --help            show this help message and exit
  -d, --disarm          track faces but do not fire any missiles
  -r, --reset           reset the turret position and exit
  --nd, --no-display    do not display captured images
  -c NUM, --camera=NUM  specify the camera # to use. Default: 0
  -s WIDTHxHEIGHT, --size=WIDTHxHEIGHT
                        image dimensions (recommended: 320x240 or 640x480).
                        Default: 320x240
  -b SIZE, --buffer=SIZE
                        size of camera buffer. Default: 2
  -v, --verbose         detailed output, including timing information
```
