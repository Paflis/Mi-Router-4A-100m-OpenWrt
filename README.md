# OpenWrt Custom Firmware Flash Tool (Xiaomi Mi Router 4A)

Automated exploit and flashing utility for deploying custom OpenWrt firmware on Xiaomi Mi Router 4A hardware.

---

## Step 1: Update & Install Dependencies

### Refresh package lists and upgrade system packages
```bash
sudo apt update
sudo apt dist-upgrade -y
```

### Install git and Python dependencies
```bash
sudo apt install git python3 python3-pip python3-venv python3-full -y
```

---

## Step 2: Clone the Repository

### Clone the OpenWRTInvasion repository
```bash
git clone [https://github.com/acecilia/OpenWRTInvasion.git](https://github.com/acecilia/OpenWRTInvasion.git)
```

### Enter the repository directory, create a virtual environment, and install Python requirements
```bash
cd OpenWRTInvasion/
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

---

## Step 3: Run the Exploit Script

### Execute the remote command execution vulnerability script
```bash
python3 remote_command_execution_vulnerability.py
```

### Input target router IP address when prompted
```bash
192.168.31.1
```

### Enter your router admin login password
```bash
mypassword
```

### Select exploit mode option 1 or 2 (preferable)
```bash
2
```

### Transfer the firmware image to the router's /tmp directory via WinSCP and rename it to openwrt.bin
```bash
openwrt-25.12.6-ramips-mt7621-xiaomi_mi-router-4a-gigabit-squashfs-sysupgrade.bin
```

---

## Step 4: Flash Firmware

### Navigate to the temporary RAM directory
```bash
cd /tmp
```

### List directory contents to verify the firmware file is present
```bash
ls -la
```

### Erase the OS1 partition, write the custom firmware binary, and reboot
```bash
mtd -e OS1 -r write openwrt.bin OS1
```

## Step 5: Configure Network via SSH

### Establish an SSH connection to the newly flashed OpenWrt router
```bash
ssh root@192.168.1.1
```

### Update the local area network IP address configuration
```bash
uci set network.lan.ipaddr='192.168.69.69'
```

### Commit the network configuration changes
```bash
uci commit network
```

### Restart the networking service to apply changes
```bash
/etc/init.d/network restart
```

<img width="1811" height="6433" alt="null" src="https://github.com/user-attachments/assets/2feaea4f-4c58-45ea-ba2d-f5d6211aff76" />
