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
Plug into Ethernet then wait for the IP to show up.
SSH into the Pi using: ssh pi@<hostname>.local


