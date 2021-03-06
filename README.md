# Robin-Pi (Needs Better Name)
Tools and Software for Gadget Mode Raspberry Pi Zero W devices

A PPCC Career Start Cyber Security project

Default Hardware:
 * Raspberry Pi Zero W
 * Zero Stem for Pi Zero
 * Adafruit 128x64 OLED Bonnet for Raspberry Pi
  
# SETUP:

Enabling SSH over USB
   
  Mount the micro sd card containing your operating system, using an adapter if necessary
  
  Open the Boot partition    
  
  Create a new, empty file named ssh in the top level directory of Boot
    
Enabling Ethernet Gadget mode
  
   Open config.txt, and add the following on a new line:
  
    dtoverlay=dwc2
  
   Open cmdline.txt, and add the following at the end of the first line:
   
    modules-load=dwc2,g_ether
    
# CONNECTING:

By USB Stem:
  Plug your raspberry pi gadget directly into a powered USB port
  
  By Micro USB Cable:
    Plug your Micro USB cable into the micro USB port closest to the middle of the board. If you have your USB Stem installed, it'll be at the end of the red arm labelled D+ D-.

DO NOT USE BOTH CONNECTION METHODS AT THE SAME TIME!

To WiFi:

  Type the following command to open the Raspberry Pi Configuration Utility:
 
    sudo raspi-config
    
  Highlight the second line for Network Options, and press enter
  
  If prompted for your country, scroll allllllll the way down to United States, then press enter
  
  If you're on the PPCC campus, your SSID will be:
  
    PPCC GUEST
    
  ... and there won't be a password. You'll have to supply the correct SSID/Passkey for other networks you try to connect to, however
  Back at the raspi-config menu, press right twice, then press enter when FINISH is highlighted
  
  Reboot if requested, or test your WiFi connection by typing:
  
    ping google.com
    
  Linux will ping forever, so kill it with ctrl-c

To OLED Bonnet:

    sudo raspi-config
  
  Highlight 5 Interfacing Options and press enter

  Highlight A5 I2C and press enter

  Highlight Yes and press enter

  Reboot with:
 
    sudo reboot

# INSTALLING REQUIRED DEPENDENCIES
 (Adapted from https://learn.adafruit.com/adafruit-128x64-oled-bonnet-for-raspberry-pi/usage)
  
# RPi.GPIO

  From the bash shell:

    sudo apt-get update

    sudo apt-get install build-essential python-dev python-pip

    sudo pip install RPi.GPIO

# Python Imaging Library

    sudo apt-get install python-imaging python-smbus i2c-tools

# Adafruit SSD1306 python library code

    sudo apt-get install git
  
    git clone https://github.com/adafruit/Adafruit_Python_SSD1306.git
  
    cd Adafruit_Python_SSD1306
  
    sudo python setup.py install
  
# TESTING YOUR SCREEN AND BUTTONS:
  
  cd to the Adafruit_Python_SSD1306 folder, then run:
  
    sudo python examples/buttons.py
  
  Try the other scripts in the examples directory, then read through the code to see how they work
    
# STARTING SCRIPTS ON BOOT:

  Add commands on new lines in /etc/rc.local to run those commands when the RPi0W boots, such as the stats demo:
  
    sudo nano /etc/rc.local
  
  Add this line before the line containing "exit 0"
 
    sudo python /home/pi/Adafruit_Python_SSD1306/examples/stats.py  &
 
  Then ctrl-o enter ctrl-x to save and quit
  
# TRANSFERING FILES FROM YOUR PI

  Install proftp:
    
    sudo apt install proftpd
    sudo service proftpd reload
    
  Connect to proftpd server from host computer (in-browser):
  
    ftp://(your USB IP address)
  
  
  
  
