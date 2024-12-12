PI5-PWNAGOTCHI-GPS
This project integrates GPS functionality with Pwnagotchi on a Raspberry Pi 5, allowing you to track the device’s location while running network operations. The setup also allows for iPhone pairing and plugin customization. 

Prerequisites
Raspberry Pi 5: Your main device for running Pwnagotchi.
U-Blox GPS Module: Used for location tracking.
MicroSD Card (16GB or more): To flash the Pwnagotchi firmware.
Pwnagotchi firmware: The software for Pwnagotchi (download from GitHub).
iPhone: Optional for pairing with the Raspberry Pi for additional functionality.
Ethernet cable and Wi-Fi access point: For network connectivity during the setup.

Step-by-Step Setup
1. Download Jayofelony’s Pwnagotchi Image
Download from the v2.8.9 release page.
2. Flash Using Raspberry Pi Imager
Download Raspberry Pi Imager.
Select "Use Custom" and choose Jayofelony’s image.
Click the settings gear icon to enable SSH, set hostname, and configure SSH login.
Write the image to your SD card.
Drop the configuration file from the GitHub repo into the boot partition of the flashed SD card.
3. Boot and SSH
Insert the SD card into your Raspberry Pi 5 and power it on.
Plug into Ethernet then wait for the IP on fing to show up.
SSH into the Pi using: ssh pi@<hostname>.local
4. Once logged in, open the SSH configuration file by running:
sudo nano /etc/ssh/sshd_config
Modify the PermitRootLogin Setting:
PermitRootLogin prohibit-password
Find the following line in the configuration file:
PermitRootLogin prohibit-password
Change it to:
PermitRootLogin yes
This allows root login using passwords, as well as keys. It's generally not recommended for security reasons, but may be necessary for this configurations.
Set the Root Password: sudo passwd root
You'll be prompted to enter and confirm the new password for the root user.
5. Open FileZilla:
Download and install FileZilla if you don’t have it already. Open it once installed.
Set Up a New SFTP Connection:
-------------------------------
Host: <your-pwnagotchi-ip-address>
Port: 22
Protocol: SFTP - SSH File Transfer Protocol
Logon Type: Normal
User: root
Password: The password you set for the root user with sudo passwd root
-------------------------------
Click Connect. If it’s your first time connecting, you may get a warning about the server's host key. Accept it to proceed.
Upload Plugins to the Custom Plugins Directory:
Once connected, in the FileZilla window, 
navigate to the 
following directory on your Pwnagotchi:
___________________________________
/usr/local/share/pwnagotchi/custom-plugins
___________________________________
On the left side of the FileZilla window (your local machine), navigate to the directory where you've stored the plugins you want to upload (from GitHub unzip if not done*).
Drag and drop all the plugins from your local folder into the custom-plugins directory on your Pwnagotchi.
Reboot the Pwnagotchi:
After transferring all the plugins, reboot your Pwnagotchi to apply the changes. You can do this by logging in via SSH again and running 
the following command:
_____________
sudo reboot
_____________
6.To use the U-Blox GPS module in your setup, the configuration is preset with the correct values. However, you’ll still need to download
the GPS client by running the following command:
____________________
sudo apt-get install gpsd gpsd-clients
____________________
Once the client is installed, everything else is ready to go. If you're using a different USB GPS device, check the log files afterward to verify a successful connection and will have to set the path for it as well:
______________
sudo journalctl -u gpsd
______________
********** you’ll need to reboot through the WebConfig interface, as a regular reboot doesn't always enable the GPS properly. Rebooting through WebConfig ensures the GPS starts working as expected after the green light comes on.**********

7. a.Turn on your iPhone’s Personal Hotspot
Ensure your iPhone’s personal hotspot is on, and Bluetooth is enabled.

b. SSH into your Pwnagotchi
From your computer’s terminal, connect to your Pwnagotchi using SSH:
ssh pi@<pwnagotchi-ip>
Replace <pwnagotchi-ip> with your Pwnagotchi’s IP address.

c. Run BluetoothCTL
Once you’re logged in, start the Bluetooth control tool by entering:
sudo bluetoothctl
 
d. Start Scanning for Bluetooth Devices
Inside the Bluetooth control tool,
begin scanning for devices:
scan on

Look for your iPhone by its name or MAC address (you’ll need the MAC address).

e. Pair Your iPhone with Pwnagotchi
Once you have your iPhone’s Bluetooth MAC address, use the following command to pair:

pair mac
Replace mac with your iPhone’s Bluetooth MAC address.

f. Trust the iPhone
After pairing, mark your iPhone as trusted:

trust mac

g. Allow Communication on Your iPhone
You should get a prompt on your iPhone asking to allow communication with the Pwnagotchi. Accept this request.

h. Troubleshooting
If the pairing fails or there's an issue, try:

Untrusting the device:

untrust mac
Unpairing the device:

remove mac
Rebooting both the iPhone and Pwnagotchi, and repeat the steps.


Plugin HUD Tweak Settings
Settings Overview
This section outlines the settings applied for the counter plugin HUD tweak. 

HUD Settings

Label: "Deauth: "
Font Style: Bold
Label Spacing: 5
Text Font: Medium
Value: "29" (example value)
Color: White (255)
Position (xy): 75, 96  <--------- 
 Assocs Metric Display

Label: "Assocs: "
Font Style: Bold
Label Spacing: 5
Text Font: Medium
Value: "678" (example value)
Color: White (255)
Position (xy): 5, 96  <--------- 
Example Layout
-----------------
Deauth: 29
Assocs: 678
-----------------
LabeledValue: sattelites
sattelites.color: 
255

sattelites.label: 
SAT:

sattelites.label_font: 
Small
sattelites.label_spacing: 
5

sattelites.text_font: 
Small
sattelites.value = "0"
sattelites.xy: 
127,83 <---------
-----------------
 
 
memtemp_header.xy: 
175,96 <---------

 
  
memtemp_data.xy: 
175,86 <---------
-----------------
