# ========= Line by Line Guide =========

## Step 1: Update & Install Dependencies
``bash
sudo apt update
sudo apt dist-upgrade -y
sudo apt install git python3 python3-pip -y

## Step 2: Clone the Repository
``bash
git clone https://github.com/acecilia/OpenWRTInvasion.git
cd OpenWRTInvasion/
pip3 install -r requirements.txt

## Step 3: Run the Exploit Script
``bash
python3 remote_command_execution_vulnerability.py
192.168.31.1
newpassword
2

## Step 4: Connect via Telnet
``bash
telnet 192.168.31.1
root
root

## Step 5: Flash Firmware
``bash
cd /tmp
ls -la
mtd -e OS1 -r write openfirm.bin OS1

## Step 6: Configure Network via SSH
``bash
ssh root@192.168.1.1
uci set network.lan.ipaddr='192.168.69.69'
uci commit network
/etc/init.d/network restart


