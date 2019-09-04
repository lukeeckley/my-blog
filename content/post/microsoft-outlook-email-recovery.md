---
title: "Microsoft Outlook Email Recovery"
date: 2018-05-08T08:11:41-07:00
draft: true
---
I recently had the opportunity to recover email messages from a computer. The computer was no longer bootable but I could access the files on the drive. The computer also had Outlook installed and configured. When Outlook is configured it creates an offline data file (OST) with a copy of your mailbox. Mail recovery is possible using this offline data file. There is a library available that allows us to interact with the OST file called [libpff](https://github.com/libyal/libpff). Using this library isn't always easy and there is a plethora of paid software available, most likely using this library, advertising the ability to recover email from an Outlook data file. I'm going to use this library in the least painful method to recover email messages - using python.

## Prerequisites
I want this to be as easy and straight forward as possible. Libpff is a library so there are numerous methods for using it, but I'm going to try my best to give you a step by step approach so that it is easily repeatable.

I'm performing this analysis on a Windows 10 computer. I'm also assuming Python is installed in `C:\Python27`.

1. Install Python 2.x - [Download](https://www.python.org/downloads/)  
Make sure you install pip because we will be using that to install the python module. The default setting during installation *is* to install pip so you should be good.
2. Update pip  
`C:\Python27\> python.exe -m pip install --upgrade pip`
3. Install the libpff python module  
Using the correct pip (it is located at C:\Python27\Scripts\pip on my PC) run the following command.
4. something  
