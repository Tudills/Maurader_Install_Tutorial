# Marauder Install Tutorial (CYD)

Guide for installing **justcallmekoko’s ESP32 Marauder** on a CYD (Cheap Yellow Display).

Originally written to help a friend. Will expand over time with tweaks and experiments.

---

## Table of Contents

1. [Setup](#1-setup)
2. [Flashing Marauder](#2-flashing-marauder)
3. [Alternative Method](#3-Alternative-Method)

---

# 1. Setup

## Install USB to UART Drivers

Download the Silicon Labs USB to UART drivers:

https://www.silabs.com/software-and-tools/usb-to-uart-bridge-vcp-drivers

After installing, restart your PC.  
Not strictly required — but drivers + Windows = I don’t argue.

---

## Verify Your COM Port

Plug in your CYD (USB-C worked for me).

Open **Device Manager** and look under **Ports (COM & LPT)**.

You should see something like this:

![Device Manager](https://github.com/Tudills/Maurader_Install_Tutorial/blob/main/Mauraders/Device%20Manager.jpg)

Take note of the COM port number.  
Example: mine is `COM15`.

Yours will likely be different.

---

## Verify Python

Open **PowerShell** and run:

```powershell
python --version
```

You should see something like:

![Python Version](https://github.com/Tudills/Maurader_Install_Tutorial/blob/main/Mauraders/python%20--version.jpg)

If you don’t have Python installed:

```powershell
winget install Python.Python.3 --scope machine
```

---

## Erase the ESP32 Flash

We’re going to fully wipe the board.  
Some CYDs ship with strange factory images.

Run:

```powershell
python -m esptool --chip esp32 --port COM15 erase_flash
```

Replace `COM15` with your actual COM port.

Example factory image:

![Factory Image](https://github.com/Tudills/Maurader_Install_Tutorial/blob/main/Mauraders/factory%20image.jpg)

---

### Enter Boot Mode

When you run the command, it will say **Connecting…**

On the back of the CYD, there are two buttons:

- Boot  
- Reset  

![Buttons](https://github.com/Tudills/Maurader_Install_Tutorial/blob/main/Mauraders/esp32%20back.jpg)

Do this:

1. Hold **Boot**
2. Press **Reset**
3. Release **Reset**
4. Release **Boot**

You’ll see something like this when erase completes:

![Erase Complete](https://github.com/Tudills/Maurader_Install_Tutorial/blob/main/Mauraders/Powershell%20Erase.jpg)

---

# 2. Flashing Marauder

## Open ESP Web Tool

Go here:

https://esptool.spacehuhn.com/

Click **Connect** (it should auto-detect).

![ESPTool Web](https://github.com/Tudills/Maurader_Install_Tutorial/blob/main/Mauraders/ESPtool%20Spacehuhn.jpg)

You’ll see several address fields like:

```
0x____
```

Example layout:

![ESPTool Setup](https://github.com/Tudills/Maurader_Install_Tutorial/blob/main/Mauraders/ESPtool%20Spacehuhn%20Setup.jpg)

---

## Get Required Files

Open the Marauder firmware wiki:

https://github.com/justcallmekoko/ESP32Marauder/wiki/update-firmware

From the table, download:

- Bootloader → `0x1000`
- Partitions → `0x8000`
- Boot App → `0xE000`

![Bootloader Partitions Boot App](https://github.com/Tudills/Maurader_Install_Tutorial/blob/main/Mauraders/Bootloader%2C%20Partitions%2C%20Boot%20App%2C%20Firmware.jpg)

Now go to Releases:

https://github.com/justcallmekoko/ESP32Marauder/releases

Scroll to **Assets**.

![Assets](https://github.com/Tudills/Maurader_Install_Tutorial/blob/main/Mauraders/Assets.jpg)

Select:

```
esp32_marauder_v1_10_3_beta_20260221_cyd_243S028_2usb.bin
```

![Correct File](https://github.com/Tudills/Maurader_Install_Tutorial/blob/main/Mauraders/ESP32%20maurader%201.jpg)

---

## Load Files into ESP Web Tool

Match each file to its correct address in ESP Web Tool exactly like this:

![Correct Layout](https://github.com/Tudills/Maurader_Install_Tutorial/blob/main/Mauraders/Look%20like%20this.jpg)

Then click **Program**.

It will take a few minutes.

When finished, you’ll see:

![Finished](https://github.com/Tudills/Maurader_Install_Tutorial/blob/main/Mauraders/finished.jpg)

---

Unplug the CYD.  
Plug it back in.
Party

---

# 3. Alternative Method

The stock CYD firmware uses a two-button interface:  
even though we got a whole touch screen... two touch actions... no no no.

If you want to try another method:

https://codehedge.github.io/Adafruit_WebSerial_ESPTool/

This must also be done using Chrome or Edge.
This thing rules.

[Webflasher](https://github.com/Tudills/Maurader_Install_Tutorial/blob/main/Mauraders/2nd%20iteration/WebFlasher.jpg)

Before using this method, I recommend performing the full PowerShell erase process first.

When connecting, you may need to practice the Boot/Reset timing. It can be tricky.

Once flashing completes, it will say:

"Flash process completed!"

Reboot or unplug and plug it back in.

You should now be greeted with Marauder running on your CYD.

Witness the glory.
[Success](https://github.com/Tudills/Maurader_Install_Tutorial/blob/main/Mauraders/2nd%20iteration/Success.jpg)
