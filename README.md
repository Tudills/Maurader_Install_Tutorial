# Maurader_Install_Tutorial
The installs of justcallmekokos ESP32  Mauraders


## Intro ##
The primary function of this readme is purely to assist my friend install justcallmekokos ESP32mauraders on a CYD. As time goes on I'll be expanding this page for proposed alterations that we discuss.

---

## **Table of Contents** ##
1. Set Up.
2. Doing the Actual Thing.

---

** 1. Set Up **

First off, download the [USB to UART drivers](https://www.silabs.com/software-and-tools/usb-to-uart-bridge-vcp-drivers)
I don't know man, probably restart your pc for spits and gigs. I just like to do that sometimes to ensure. You know, Driver stuff. Anyway. Plug in your CYD, I used USB-C. Open up *'Device Manager'* 


 ![Device Manager](<img width="158" height="217" alt="Device Manager" src="https://github.com/user-attachments/assets/35fb8db9-b7e9-44eb-85ac-62b306169c16" />)

You want to see something like this (your COM port wont be as high as mine for sure, I got 3 million things plugged into my comp, But it's what we are gonna need to know. For example mine is COM15. 

Open up Windows Powershell
Make sure you have python installed,

'python --version'

if you don't

 'winget install Python.Python.3 --scope machine'

take note of the COM port your esp32(cyd) is on. Pop in this command.

'python -m esptool --chip esp32 --port COM15 erase_flash'

for COM15 you'll have to replace your snippit of code for your own COM port.

all we are doing here is just erasing everything that was on these little guys. Sometimes they ship with somesort of weird factory image. ![Factory Image](image.jpg)

So when you run that command, on the back of the CYD, There is 2 Buttons. "Boot" "Reset"

There will be a text box that says connecting. The connecting text will exist for about 10 seconds ![Connecting](image.jpg). Hold 'boot' and while holding it, press 'reset' let go of 'reset' and then let go of 'boot'.
so kinda,

-hold boot
-press reset
-let go of boot

I know it seems a bit much. But, trust me. It's going to feel better knowing the entire thing is cleared out.
![Powershell Erase](image.jpg)

---

2. Doing the actual thing.

Alright, so lets go to this website,  [Esptool Spacehuhn](https://esptool.spacehuhn.com/)
![ESPtool Spacehuhn](image.jpg) I circled connect in case you are braindead. It should Autoconnect.

What will show up now is a series of boxes that say 
0x
(and then some value)

It will look something like this.
![ESPtool Spacehuhn Setup](image.jpg)

Open up another tab and go to justcallmekokos github, there is a page about updating firmware ![Here](https://github.com/justcallmekoko/ESP32Marauder/wiki/update-firmware)

Grab these files from this table.
-Bootloader 0x1000
-Partitions 0x8000
-Boot App 0xE000

The Firmware we are going to grab from justcallmekokos most recent ![releases] (https://github.com/justcallmekoko/ESP32Marauder/releases) and scroll down untill you see "Assets"
![Assets](image.jpg) 

Select the "esp32_marauder_v1_10_3_beta_20260221_cyd_243S028_2usb"

With each of those files, put them into the ESPWEBTOOL just like how they are in this photo. ![Look like this](image.jpg)

hit "program"

It will take a couple minutes, it will finish and look like this ![Finish](image.jpg) 

unplug that bad boy from the comp... plug it back in. witness the glory.
