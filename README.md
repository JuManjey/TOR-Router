# TOR-Router <br>
Make your own TOR Router with RaspberryPi <br>
**1. Setup  Raspberry Pi OS on SD-card** <br>
https://www.raspberrypi.com/software/ <br>
**2. Before inserting SD-card to RPi, in main directory make file with name 'ssh'** <br>
**3. Connect to RaspberryPi with default creditionals: pi/raspberry** <br>
**4. First - Update** <br>
sudo apt-get update && sudo apt-get upgrade && sudo apt-get install git <br>
**5.Change the default password** <br>
passwd pi <br>
**6. Setup Wireless** <br>
git clone https://github.com/unixabg/RPI-Wireless-Hotspot.git <br>
cd RPI-Wireless-Hotspot <br>
sudo ./install <br>
"Y" to agree to terms <br>
"Y" to use preconfigured DNS <br>
"Y" to use Unblock-Us DNS servers <br>
"N" for WiFi defaults <br>
Type in a new WiFi password (it will be checked) <br>
Type in a new SSID <br>
Type in your desired WiFi channel (1, 6, 11) <br>
Type "N" when asked - "Are you using a rtl871x chipset?" <br>
Type "N" for chromecast support (unless you plan to use a chromecast w/RasTor) <br>
**If you have the: "Failed to start hostapd.service: Unit hostapd.service is masked."** <br>
sudo systemctl unmask hostapd <br>
sudo systemctl enable hostapd <br>
sudo systemctl start hostapd <br>
**REBOOT**
Now you can test your wifi
Connect to RPi-Wireless and test the connection. RPi must work like wireless point
**Install TOR Service**
sudo apt-get install tor
sudo nano /etc/tor/torrc
**Add this lines after the first paragraph**
Log notice file /var/log/tor/notices.log
VirtualAddrNetwork 10.192.0.0/10
AutomapHostsSuffixes .onion,.exit
AutomapHostsOnResolve 1
TransPort 192.168.42.1:9040
TransListenAddress 192.168.42.1
DNSPort 192.168.42.1:53
DNSListenAddress 192.168.42.1
**Configure iptables**
sudo iptables -F && sudo iptables -t nat -F <br>
sudo iptables -t nat -A PREROUTING -i wlan0 -p udp --dport 53 -j REDIRECT --to-ports 53 <br>
sudo iptables -t nat -A PREROUTING -i wlan0 -p tcp --syn -j REDIRECT --to-ports 9040 <br>
**Check iptables**
sudo iptables -t nat -L
sudo sh -c "iptables-save > /etc/iptables.ipv4.nat"
**Create log file (If you need)**
sudo touch /var/log/tor/notices.log <br>
sudo chown debian-tor /var/log/tor/notices.log && sudo chmod 644 /var/log/tor/notices.log <br>
**Start TOR service**
sudo service tor start
**Check to see if the service is running:**
sudo service tor status
**Run TOR Service at Boot:**
sudo update-rc.d tor enable
**REBOOT**
sudo reboot

That`s all! Connect to wireless of your RPi and check your ip with 2ip.ua
