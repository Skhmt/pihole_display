# Follow these instructions to make the display work as a console output (NOT for use with Pi-hole):

Update your OS:

	sudo apt update -y
	sudo apt upgrade -y

Get operating system packages:

	sudo apt-get install -y git python3-venv python3-pip

Create a virtual environment named "env":

	cd ~
	python -m venv env --system-site-packages
	source env/bin/activate

Once the virtual environment is activated, run this to install other modules:

	pip3 install --upgrade adafruit-python-shell click

To install the kernel-module console output, run:

	git clone https://github.com/adafruit/Raspberry-Pi-Installer-Scripts.git
	cd Raspberry-Pi-Installer-Scripts

Then for the 1.14" two-button screen, run:

	sudo -E env PATH=$PATH python3 adafruit-pitft.py --display=st7789_240x135 --rotation=270 --install-type=console

Alternatively for the 1.3" joystick and two-button screen, run: 

	sudo -E env PATH=$PATH python3 adafruit-pitft.py --display=st7789v_bonnet_240x240 --rotation=0 --install-type=console

If you have to uninstall, run:

	cd ~
	source env/bin/activate
	cd Raspberry-Pi-Installer-Scripts
	sudo -E env PATH=$PATH python3 adafruit-pitft.py --install-type=uninstall
