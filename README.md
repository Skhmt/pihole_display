# Install the Raspberry Pi OS

Get the Imager from:

	https://www.raspberrypi.com/software/

1. Select Raspberry Pi Zero (bottom of the list, NOT "Raspberry Pi Zero 2 W")
2. Select Raspberry Pi OS (Legacy, 32-bit) (second from top of the list)
3. Select the USB stick (something like: "Generic MassStorageClass USB Device - 29.5 GB")
4. Enter a hostname - remember this
5. Select "Washington, D.C.", "America/Los_Angeles", and "us"
6. Choose a username and password - remember these 
	(you can always re-run the install process if you forget, which wipes out everything)
7. Enter your wifi network SSID and password - it must be a 2.4 Ghz network, not 5 Ghz
8. Enable SSH and select "Use password authentication"
9. Do not enable Raspberry Pi Connect
10. Click "Write" and wait a while

After it's done, put the SD card into the Raspberry Pi Zero W and insert the power
mini USB into the "PWR IN" connector on the bottom right.

Let the green light stop blinking, perhaps 10 minutes or so the first time you do this and 1-2 minutes subsequently.

Go into a computer that is on the same WiFi network and open the console or command prompt or Power Shell.

Try the following without [brackets]:

	ping [hostname from before].local

If you get replies, that's good. If not, wait a few minutes and try again.
If it still doesn't work after the green light has been solid for a while, you may have originally entered your
SSID or password incorrectly or are using a 5 Ghz network instead of a 2.4 Ghz (802.11 a/c/n) network.

Enter the following without [brackets]:

	ssh [username from before]@[hostname from before].local

Enter the password from before for your username.

Update your OS:

	sudo apt update -y
	sudo apt upgrade -y

## Pi-hole adblocker install after re-SSHing:

	curl -sSL https://install.pi-hole.net | bash

> [!TIP]
> Uninstall Pi-hole with: `sudo pihole uninstall`

## For python output with pihole

	sudo apt install python3-venv
	sudo apt-get install -y python3-pip
	python3 -m venv pihole --system-site-packages
	source pihole/bin/activate
	pip3 install --upgrade adafruit-python-shell
	wget https://raw.githubusercontent.com/adafruit/Raspberry-Pi-Installer-Scripts/master/raspi-blinka.py
	sudo -E env PATH=$PATH python3 raspi-blinka.py

After restart (you have to run the first line every time you restart or reconnect):

	source pihole/bin/activate
	pip3 install adafruit-circuitpython-rgb-display
	sudo apt-get install fonts-dejavu python3-pil python3-numpy

Get the stats.py file:

	wget https://gist.githubusercontent.com/Skhmt/e390d9a891482ca548c60530a200811d/raw/c9c533c13d718bcf3164260ce03bfd1dc20382c8/stats.py

Remove the password from pihole:

	sudo pihole setpassword

	(then hit enter for a blank password)

Run it:

	python3 stats.py

Make it automatically run:

	sudo nano /etc/rc.local

Add this new line before "exit 0":

	sudo ~/pihole/bin/python3 ~/stats.py &
	
Ctrl+X to exit, Y to save, then hit enter

# Sources for these instructions

- Very outdated instructions: https://learn.adafruit.com/pi-hole-ad-blocker-with-pi-zero-w?view=all#install-mini-pitft
- For more in-depth instructions on Pi-hole, see: https://github.com/pi-hole/pi-hole/#one-step-automated-install
- Better 1.14" instructions, but doesn't include Pi-hole and screen instructions: https://learn.adafruit.com/adafruit-mini-pitft-135x240-color-tft-add-on-for-raspberry-pi/kernel-module-install
- 1.3" screen instructions: https://cdn-learn.adafruit.com/downloads/pdf/adafruit-1-3-color-tft-bonnet-for-raspberry-pi.pdf
- 2.13" e-ink: https://www.waveshare.com/wiki/2.13inch_e-Paper_HAT_Manual#Working_With_Raspberry_Pi
