# Machine Configuration and Repository Usage Guide

This guide will walk you through preparing your machine, enabling necessary services, and setting up the environment using the provided repository.

## Prerequisites

### If using CT
1. **Enable NFS and Samba**:
   To enable Network File System (NFS) and Samba for file sharing, follow the instructions provided by your operating system's documentation.

2. **Keep privileges**:
   Ensure you have the necessary privileges to perform administrative tasks.

3. **Mount Proxmox pool to `/mnt/rust`**:
   Mount your Proxmox storage pool to `/mnt/rust` using appropriate mount commands or your system's GUI.

## Preparing the Operating System

1. Prepare the OS using the following Ansible setup:
   [GitHub Repository - aviellg/ansible-pull-setup](https://github.com/aviellg/ansible-pull-setup)

2. Run the setup script:
```bash
#!/bin/bash

echo "Running setup script..."

# Install cockpit
sudo apt update
sudo apt install -y cockpit

# Fetch and run the setup script from 45Drives
curl -sSL https://repo.45drives.com/setup | sudo bash

# Update the package list
sudo apt update

# Install cockpit identities
sudo apt install -y cockpit-identities

# Download the cockpit-file-sharing package
curl -LO https://github.com/45Drives/cockpit-file-sharing/releases/download/v4.2.8/cockpit-file-sharing_4.2.8-1focal_all.deb

# Install the cockpit-file-sharing package
sudo apt install -y ./cockpit-file-sharing_4.2.8-1focal_all.deb

# Download the cockpit-navigator package
wget https://github.com/45Drives/cockpit-navigator/releases/download/v0.5.10/cockpit-navigator_0.5.10-1focal_all.deb

# Install the cockpit-navigator package
sudo apt install -y ./cockpit-navigator_0.5.10-1focal_all.deb

# Prompt user for autoadmin password
read -sp 'Enter password for autoadmin: ' password

# Configuring the autoadmin user
echo -e "${password}\n${password}" | sudo passwd autoadmin

echo "Setup complete!"
```
3. Connecting to Cockpit
   After running the setup script, you can connect to Cockpit using the following URL:

   https://servername.lan:9090/
   Replace servername.lan with the actual hostname or IP address of your machine.
