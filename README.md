# Line by Line Guide

## Step 1: Update & Install Dependencies
```bash
sudo apt update
sudo apt dist-upgrade -y
sudo apt install git python3 python3-pip -y

git clone https://github.com/acecilia/OpenWRTInvasion.git
cd OpenWRTInvasion/
pip3 install -r requirements.txt

python3 remote_command_execution_vulnerability.py 192.168.31.1 newpassword 2

telnet 192.168.31.1
# login: root | password: root

cd /tmp
ls -la
mtd -e OS1 -r write openfirm.bin OS1

ssh root@192.168.1.1

uci set network.lan.ipaddr='192.168.69.69'
uci commit network
/etc/init.d/network restart


---

✨ This way:
- Commands are clearly separated inside **bash code blocks**.
- Steps are structured with **headings**.
- It’s easy to follow line by line.

---

👉 Do you want me to also **embed your screenshot** at the end of the README (like in your first example) so that people can see the success output?
