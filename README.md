# Stealthchanger-Setup
Setup for my Stealthchanger
Install RaspiOS 64bit Lite
Log in via SSH

I am utilising a Kraken Controller, Raspberry Pi 4B+ with a USB SSD


Run:
```
sudo apt update
```
Run:
```
sudo apt upgrade
```
Install Git by Running:
```
sudo apt install git
```
Install Klipper by Running:
```
cd ~
git clone https://github.com/th33xitus/kiauh.git
./kiauh/kiauh.sh
```
Install Klipper, Moonraker, Mainsail and Crowsnest
Run:
```
uname -a
```
Enable CAN Network by Running:
```
sudo systemctl enable systemd-networkd
```
Run to start it:
```
sudo systemctl start systemd-networkd
```
Run to make sure its running:
```
systemctl | grep systemd-networkd
```
Disable the Online Wait Service by Running:
```
sudo systemctl disable systemd-networkd-wait-online.service
```
Setup the TX Que Length by running:
```
echo -e 'SUBSYSTEM=="net", ACTION=="change|add", KERNEL=="can*"  ATTR{tx_queue_len}="128"' | sudo tee /etc/udev/rules.d/10-can.rules > /dev/null
```
Confirm it by running:
```
cat /etc/udev/rules.d/10-can.rules
```
Set speed to 100000 and start it by running:
```
echo -e "[Match]\nName=can*\n\n[CAN]\nBitRate=1M\nRestartSec=0.1s\n\n[Link]\nRequiredForOnline=no" | sudo tee /etc/systemd/network/25-can.network > /dev/null
```
Confirm it has been applied correctly:
```
cat /etc/systemd/network/25-can.network
```
Now Reboot by running:
```
sudo reboot now
```
Install the latest Python:
```
sudo apt update
sudo apt upgrade
sudo apt install python3 python3-serial
```
Install Katapult:
```
test -e ~/katapult && (cd ~/katapult && git pull) || (cd ~ && git clone https://github.com/Arksine/katapult) ; cd ~
```
Flash Mainboard and Toolheads using Esotericals guide at https://https://canbus.esoterical.online/
Install Klipper Toolchanger by running:
```
wget -O - https://raw.githubusercontent.com/viesturz/klipper-toolchanger/main/install.sh | bash
```
Insert the follow at the end of your Moonraker.conf to enable it be added to the update options
```
[update_manager klipper-toolchanger]
type: git_repo
channel: dev
path: ~/klipper-toolchanger
origin: https://github.com/viesturz/klipper-toolchanger.git
managed_services: klipper
primary_branch: main
```
Utilise the Config files in your printer setup from the Config Directory

Have Fun
