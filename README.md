# TOR-Router
Make your own TOR Router with RaspberryPi

**1. Setup  Raspberry Pi OS on SD-card**
https://www.raspberrypi.com/software/

**2. Before inserting SD-card to RPi, in main directory make file with name 'ssh'**

**3. Connect to RaspberryPi with default creditionals: pi/raspberry**

**4. First - Update**

sudo apt-get update && sudo apt-get upgrade && sudo apt-get install git

**5.Change the default password**

passwd pi

**6. Setup Wireless**

git clone https://github.com/unixabg/RPI-Wireless-Hotspot.git
cd RPI-Wireless-Hotspot
sudo ./install

"Y" to agree to terms

"Y" to use preconfigured DNS

"Y" to use Unblock-Us DNS servers

"N" for WiFi defaults

Type in a new WiFi password (it will be checked)

Type in a new SSID

Type in your desired WiFi channel (1, 6, 11)

Type "N" when asked - "Are you using a rtl871x chipset?"

Type "N" for chromecast support (unless you plan to use a chromecast w/RasTor)

**If you have the: "Failed to start hostapd.service: Unit hostapd.service is masked."**
