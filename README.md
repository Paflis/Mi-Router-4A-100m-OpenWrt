OpenWrt Custom Firmware Flash Tool (Xiaomi Mi Router 4A)

Automated exploit and flashing utility for deploying custom OpenWrt firmware on Xiaomi Mi Router 4A hardware.

Prerequisites & Setup

Ensure your local build environment (Ubuntu-based host recommended) is up to date and has the required Python runtimes installed.

# Refresh package lists and perform a safe system distribution upgrade
sudo apt update && sudo apt dist-upgrade -y

# Install git for version control and Python 3 with pip package management
sudo apt install git python3 python3-pip -y


Step 1: Clone and Prepare Repository

Pull down the exploit toolchain and install the required Python dependencies (such as requests/sockets) to execute the remote exploit payload.

# Clone the repository containing the exploit scripts
git clone https://github.com/acecilia/OpenWRTInvasion.git
cd OpenWRTInvasion/

# Install required Python libraries specified in requirements.txt
pip3 install -r requirements.txt


Step 2: Execute Remote Command Execution (RCE) Exploit

Run the RCE script against the stock firmware interface. Follow the interactive prompts to target the gateway, set your temporary root password, and trigger the vulnerability.

# Run the primary exploit script to bypass stock firmware restrictions
python3 remote_command_execution_vulnerability.py

# When prompted by the script:
# 1. Enter router IP address:
192.168.31.1

# 2. Enter your desired new root password:
newpassword

# 3. Select exploit option (typically option 2 for Telnet/SSH payload injection):
2


Step 3: Access the Router via Telnet

Once the exploit successfully executes, open an unencrypted Telnet session into the router's active busybox shell using the default or newly created credentials.

# Open a Telnet connection to the router's default recovery gateway
telnet 192.168.31.1

# Login credentials:
# Username: root
# Password: [the password you set during Step 2]


Step 4: Flash OpenWrt Firmware Image

Transfer your compiled OpenWrt image (openfirm.bin) to the router's volatile RAM partition and flash it directly to the designated flash memory partition (OS1), forcing an automatic reboot.

# Navigate to the temporary RAM directory to avoid writing to flash prematurely
cd /tmp

# Verify that your custom firmware binary is successfully staged
ls -la

# Erase the OS1 partition, write the custom bin image, and reboot (-r)
mtd -e OS1 -r write openfirm.bin OS1


Step 5: Post-Flash Network Configuration

After the router reboots into OpenWrt, the default LAN IP usually shifts to 192.168.1.1. Connect via SSH and assign your preferred static LAN subnet configuration.

# Establish an SSH session into the newly flashed OpenWrt environment
ssh root@192.168.1.1

# Modify the default LAN IP address scheme (e.g., changing to 192.168.69.69)
uci set network.lan.ipaddr='192.168.69.69'

# Commit the changes to the UCI configuration database
uci commit network

# Restart the network daemon to apply the new IP address immediately
/etc/init.d/network restart

<img width="1811" height="6433" alt="null" src="https://github.com/user-attachments/assets/2feaea4f-4c58-45ea-ba2d-f5d6211aff76" />
