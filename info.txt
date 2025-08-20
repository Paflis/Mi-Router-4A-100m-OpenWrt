# firmwares
========= Line by Line Guide installing OpenWrt =========

sudo apt update
sudo apt dist-upgrade
Y
sudo apt install git pip python3
Y
git clone https://github.com/acecilia/OpenWRTInvasion.git
cd OpenWRTInvasion/
pip3 install -r requirements.txt
python3 remote_command_execution_vulnerability.py
192.168.31.1
newpassword
2
=============================================

Transfer Openwrt firmware to /temp directory

=============================================
telnet 192.168.31.1
root
root
cd /tmp
ls -la
mtd -e OS1 -r write openfirm.bin OS1
ssh root@192.168.1.1
uci set network.lan.ipaddr='192.168.69.69'
uci commit network
/etc/init.d/network restart
