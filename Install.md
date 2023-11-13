# Installation and Configuration Guide

This document details the steps required to install necessary software, configure network settings, set up routers, and perform tests within a secure network simulation environment.

## Software Installation

### GNS3

1. Download GNS3 from [GNS3's website](https://www.gns3.com/).
2. Install GNS3 by running the downloaded executable and following the installation prompts.
3. Launch GNS3 and complete the setup wizard to integrate with VirtualBox and Wireshark.

### VirtualBox

1. Download VirtualBox from [VirtualBox's website](https://www.virtualbox.org/).
2. Execute the installer and proceed through the installation process.
3. Open VirtualBox after installation to ensure it's functioning properly.

### Wireshark

1. Download Wireshark from [Wireshark's website](https://www.wireshark.org/).
2. Run the installer and follow the on-screen instructions to install Wireshark.
3. Launch Wireshark to confirm the installation was successful.

## Network Configuration

### Setting Up Virtual Machines

1. Download pre-configured Debian VM images from [osboxes](https://www.osboxes.org/debian/).
2. In VirtualBox, go to "File" > "Import Appliance" and select the downloaded `.ova` files.
3. Follow the prompts to import the Debian VMs.

### Integrating VMs with GNS3

1. In GNS3, navigate to "Edit" > "Preferences".
2. Under the "VirtualBox" section, add the path to your VirtualBox installation.
3. Include the imported Debian VMs into your GNS3 project by selecting them from the VirtualBox VM list.

## Router Configuration

### Basic Router Setup

For each router in GNS3:

```
conf t
hostname [Router_Name]
enable secret [Password]
line vty 0 4
password [Password]
login
exit
```

Replace [Router_Name] with Paris_Router or Rennes_Router and [Password] with a secure password.

# Interface Configuration for Paris Router

```
conf t
interface e0/0
ip address 192.168.1.1 255.255.255.0
no shutdown
exit
```

# Interface Configuration for Rennes Route

```
conf t
interface e1/0
ip address 192.168.2.1 255.255.255.0
no shutdown
exit
```

# Saving Router Configurations

```
wr mem
```

 # Testing Network Configuration

 ## Connectivity Test 

 From the terminal of each VM:

 ```
ping 192.168.1.1  # From Rennes VM to Paris Router
ping 192.168.2.1  # From Paris VM to Rennes Router
```

You should receive replies if the network is configured correctly.

Traffic Analysis
Open Wireshark.
Select the network interface connected to your virtual network.
Start capturing packets.
Filter the captured traffic as necessary to analyze specific packets.
Troubleshooting
If you encounter issues:

1. Review all network settings for typos or misconfigurations.
2. Restart GNS3 and reload the router configurations.
3. Ensure that VirtualBox network settings are consistent with GNS3.

After following these detailed instructions, your network should be fully functional and ready for secure communication testing.

