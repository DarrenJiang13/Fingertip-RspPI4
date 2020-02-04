# Installation Tutorial of Raspberry PI4 with Ubuntu 18.04

This is a tutorial for installing Ubuntu 18.04 on Raspberry PI4.

## 1. What you will need
  refer to: https://projects.raspberrypi.org/en/projects/raspberry-pi-setting-up/2
  - A Raspberry Pi 4 Computer
  - A 5V 3.5A power adapter
  - A 32 GB micro SD card (for install the OS of PI4)
  - A micro SD card reader (Or any device that can make your sd card written by your computer)
  - A Micro HDMI to HDMI Adapter Cable (PI4 only has 2 micro HDMI ports as its video ouput)
  - A PI4 case (optional)
  
  Now let's start installing our system.
  
## 2. Update firmware in Raspbian
  refer to: https://projects.raspberrypi.org/en/projects/raspberry-pi-setting-up/3  
  refer to: https://jamesachambers.com/raspberry-pi-4-ubuntu-server-desktop-18-04-3-image-unofficial/
  
  Before you install the ubuntu 18.04, you need to update the firmware of PI4.
  
  Firstly you need to install Raspbian, which is the Foundation's official supported operating system for raspberry PI board.
  1. Format your micro SD card.
     - Download [SD Formatter](https://www.sdcard.org/downloads/formatter/index.html) for Windows. Use this software to format your SD card.
     - Insert your SD card into the computer or laptop’s SD card slot.
     - In SD Formatter, select your SD card, and the format the card.
  2. Install Raspian to your PI4
     - Visit the Raspberry Pi [downloads page](https://www.raspberrypi.org/downloads/). click [noobs](https://www.raspberrypi.org/downloads/noobs/) then "download zip".
     - Then extract all the files in `.zip` file directly to your micro SD card 
  3. Insert the SD card you’ve set up with Raspbian (via NOOBS) into the microSD card slot
  4. Connect HDMI cable, your mouse and keyboard to PI4
  5. Connect the power adapter, waiting for PI4 to start. Then choose Rasbian and click install.
  6. Wait for the installation to finish (30-60 minutes). Click [here](https://projects.raspberrypi.org/en/projects/raspberry-pi-setting-up/6) for more information during setting up. 
  7. Reboot the PI4. (You can either use "sudo reboot" or click the reboot button)
  
  Now you have already installed Raspbian, firmware should be updated before you installing your ubuntu.
  1. Install the latest firmware using this command:  
  
    sudo apt-get update && sudo apt-get dist-upgrade -y
    sudo rpi-update
    
  2. Check for bootloader updates:  

    sudo rpi-eeprom-update -a
    
## 3. Install Ubuntu 18.04-desktop
refer to :https://jamesachambers.com/raspberry-pi-ubuntu-server-18-04-2-installation-guide/
  Instead of installing a ubuntu server, we choose a desktop version which seems more friendly to us.
  1. Download ubuntu 18.04-desktop image from [here](https://github.com/TheRemote/Ubuntu-Server-raspi4-unofficial/releases).   
  Our version is v27 release, file name :`ubuntu-18.04.3-preinstalled-desktop-arm64+raspi4.img.xz`
  2. Extract `ubuntu-18.04.3-preinstalled-desktop-arm64+raspi4.img` outside.
  3. Use [Win32DiskImager](https://sourceforge.net/projects/win32diskimager/) to write the img to your micro SD card. 
    - Format your micro SD card first. If you have two cards, you can use one as your "Official Raspbian Image" and another to install ubuntu system.
    - Choose Image File on Win32DiskImager: select the image you have just extracted
    - Choose Device on Win32DiskImager: the location of your SD card. Select the drive on which your SD card is mounted
    - Click "write"
   4. Insert your micro SD card to the PI4 and power on!

## 4. Enjoy your Ubuntu on PI!
   At the first time when you enter into the ubuntu18.04-desktop the username would be `ubuntu` and the password would also be `ubuntu`. 
   
   When you input the password for the first time, you would be asked to set a new password.
   - firstly you need to enter in the "(current) password", which is :`ubuntu`
   - then you need to enter in your new password
   - finally retype your password
   
   Then you will see the familiar ubuntu18.04 desktop. Congratulations!
