# About Pintro

The project initial idea was to automatically track office attendance. But who would like their attendance being tracked automatically? No one would. So with the Pintro project, we decided that tracking a user should result in a direct benefit for the user. We did so by giving every team member who would enable attendance tracking a personal intro tune. So every day that they enter the office, and the system recognises them, Pintro plays them their personal intro tune (Pintro Tune)!

In this repository, we share the hardware requirements, what information you need from your colleagues and the Python code that allows you to start playing intro songs and tracking attendance in Google Analytics.

*At [Superweek](http://www.superweek.hu/) 2018, the Pintro project was a finalist for the Golden Punchcard Prize. A prize where you 'demonstrate any digital analytics solution or method of your own that is way beyond the defaults'.*

## 1. Hardware requirements
To get started with Pintro Tunes, you need hardware. For one Pintro Tunes system, you'll need:

- A Raspberry Pi (with power adapter and sd card (Raspbian)).
- A Wifi Dongle with a driver that supports monitor mode on ARM (Raspberry Pi)
    - rt2800usb is that works stable to our knowledge. For example: [Tenda W311MA](https://www.lightinthebox.com/nl/tenda-w311ma-150mbps-draadloze-n150-high-power-usb-adapter-draadloze-netwerkkaart-wifi-ontvanger-wi-fi-card-ap-functie_p5446216.html), [Tenda W322U](https://www.amazon.de/dp/B002IJA5J2/ref=pe_386171_38075861_TE_item), [Tenda W311M](https://wikidevi.com/wiki/Tenda_W311M)
    - Don't try the ath9k_htc driver, the unstable monitor mode on ARM destroyed many of our SD cards (destroyed as in: made completely useless you can't even reburn the image)
    - We found other drivers that were supposed to support monitor mode, but didn't support it on the pi (due to ARM chipset)
    - Double check whether the dongle you want to purchase truly uses the rt2800usb, sometimes a new version uses different driver (and it's often not easy to find out the exact version)
    - If anybody discovers different dongles and/or drivers that work in stable monitor mode on the Pi, please share!
- Speakers with a standard audio jack.
- To track data in Google Analytics, you need internet access (wifi or ethernet).

To set up remote access to the Pintro Tunes system (only required for your initial setup):

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

## 3. Running Pintro

Start by getting the remote IP address of your Raspberry Pi. It'll make setting up Pintro easier! When you launch your system (with a keyboard, screen and an ethernet cable connected!), hit `Ctrl+Alt+F1` to access the terminal, and type `hostname -I` to view your remote IP address. After that, use a program like Putty to access your Raspberry Pi, or use your FTP manager of choice to put files on it. 

Add `config.json` and `pintro.py` to your Raspberry Pi through FTP. 

**Configuration**

First, edit the `config.json` file. You can change the following fields:

- `pintro_area`: the area your tracking attendance in. This value will be used as the event category.
- `wlan`: the wlan interface you're using. If you have a Pi 3B or use another wifi dongle, it will probably be wlan1. If you aren't/haven't used wifi on the Pi, it will probably be wlan0. If you're not sure: the output of pintro.py when starting the monitor mode shows you which wlan has which driver, look for the wlan with rt2800usb. If the monitor mode is already running, it won't show again so use `sudo airmon-ng stop wlan0` or `sudo airmon-ng stop wlan1` if you need to stop the monitor mode.
- `max_play_time`: the maximum play time for your mp3 files.
- `google_analytics_tracking_id`: the tracking id for your GA property. Leave blank if you don't want track users.
- `mac`: the object that holds our user data. For each user list:

```
"ma:ca:dd:re:ss:01": {
  {
    "user_name":"usernamevalue",
    "mp3_name":"file.mp3"
  }
}
```

Keep in mind that the `user_name` will be used as the event action in Google Analytics. You might not want to send actual names to GA. 

**Running Pintro**

Access your Pi through [Putty](https://www.putty.org/). After that, install the following tools on your Pi:

```sudo apt-get install aircrack-ng screen tcpdump omxplayer```

You can now open a virtual screen on your Pi with the `screen` command. Now all you have to do is run the `pintro.py` file:

```
python3 pintro.py
```

When Pintro is done initialising, it should print 'start'. After that, make sure to detach yourself from the virtual screen with the `Ctrl+A+D` shortcut. If you ever want to open the virtual screen again, run `screen -r`. 


