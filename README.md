# About Pintro

The project initial idea was to automatically track office attendance. But who would like their attendance being tracked automatically? No one would. So with the Pintro project, we decided that tracking a user should result in a direct benefit for the user. We did so by giving every team member who would enable attendance tracking a personal intro tune. So every day that they enter the office, and the system recognises them, Pintro plays them their personal intro tune (Pintro Tune)!

In this repository, we share the hardware requirements, what information you need from your colleagues and the Python code that allows you to start playing intro songs and tracking attendance in Google Analytics.

*At [Superweek](http://www.superweek.hu/) 2018, the Pintro project was a finalist for the Golden Punchcard Prize. A prize where you 'demonstrate any digital analytics solution or method of your own that is way beyond the defaults'.*

# 1. Hardware requirements
To get started with Pintro Tunes, you need hardware. For one Pintro Tunes system, you'll need:

- A Raspberry Pi (with power adapter and sd card).
- A W311MA USB Wifi Dongle - [Example product link](https://www.lightinthebox.com/nl/tenda-w311ma-150mbps-draadloze-n150-high-power-usb-adapter-draadloze-netwerkkaart-wifi-ontvanger-wi-fi-card-ap-functie_p5446216.html) *You need a W311MA type dongle to sniff for WIFI MAC addresses*
- An Ethernet cable.
- Speakers with a standard audio jack.

To setup the Pintro Tunes system:

- A monitor with standard HDMI cable.
- A Keyboard.

## 2. Collecting data from  your team members

To get attendance data and give people their personal intro tune, you'll need to collect data from the people in your team. Ask your team members for:

- Full name.
- Email address.
- Youtube URL of the preferred intro tune. *You'll need to get these songs as an MP3.*
- Wifi MAC address:
  - Example Android: http://www.wikihow.com/Find-the-WiFi-Mac-Address-on-an-Android.
  - Example iOS: https://www.tekrevue.com/tip/how-to-find-mac-address-iphone-ipad/.
  
For our team, we collect this data through a Google Form, where users automatically give their consent for tracking! \#iamnotalawyer

# Running Pintro

Start by getting the remote IP address of your Raspberry Pi. When you launch your system, hit `Ctrl+Alt+F1` to access the terminal, and type `hostname -I` to view your remote IP address. After that, use a program like Putty to access your Raspbery Pi, or use your FTP manager of choice to put files on it. 


