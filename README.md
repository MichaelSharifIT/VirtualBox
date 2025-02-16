# A Primer on Provisioning Virtual Machines with VirtualBox

## Table of Contents
1. [VirtualBox Overview](#virtualbox-overview)
2. [What is VirtualBox?](#what-is-virtualbox)
3. [VirtualBox Network Settings](#virtualbox-network-settings)
4. [Download VirtualBox](#download-virtualbox)
5. [Host Key](#host-key)
6. [Provision A New NAT Network In VirtualBox](#provision-a-new-nat-network-in-virtualbox)
7. [Download ISOs](#download-isos)
8. [Provision A Virtual Machine](#provision-a-virtual-machine)
9. [Take A Snapshot](#take-a-snapshot)
10. [Restore Snapshot](#restore-snapshot)
11. [Full Screen With VirtualBox Guest Additions](#full-screen-with-virtualbox-guest-additions)
    - [Windows](#windows)
    - [Linux](#linux)

---

## VirtualBox Overview

### What is VirtualBox?
VirtualBox is a free program that lets you create virtual machines (VMs) on your computer. VirtualBox is what’s known as a Type 2 hypervisor, which basically means it runs on top of an existing operating system (like Windows, macOS, or Linux) rather than directly on the hardware. This lets you create and manage virtual machines (VMs) right from your computer without needing any extra hardware. Each VM acts like a completely separate computer, with its own operating system, applications, and network settings.

In the context of security, VirtualBox is perfect for setting up personal labs for cybersecurity practice. You can install vulnerable VMs to practice hacking skills, network configurations, or simulate small networks, all in a safe, isolated space. This is what we will be doing in this project!

---

## VirtualBox Network Settings
VirtualBox network settings give you different ways to connect your virtual machines to the internet or to each other. You can keep them isolated, connect them just to each other, or even have them act like any other device on your network.

Here’s a bit more detail on the five main VirtualBox networking settings.

1. **NAT (Network Address Translation)**: NAT is the default network mode, where VirtualBox acts like a middleman for internet access. Your virtual machine (VM) can go online, but it’s hidden from your main network and other VMs, keeping things secure and simple. Great if you just need internet access without any extra setup.

2. **NAT Network**: NAT Network is similar to regular NAT but allows multiple VMs to see each other while still keeping them hidden from the rest of your network. This is useful if you want to set up a small, private network between VMs that can also connect to the internet, like a mini-lab setup.

3. **Bridged Adapter**: Bridged Adapter connects your VM directly to your actual network, as if it were just another device on your Wi-Fi or Ethernet. The VM gets its own IP address on the network and can communicate freely with other devices. This is ideal if you want full access to your network for testing or server setups.

4. **Internal Network**: Internal Network is like having a private network that’s entirely cut off from the internet and your host machine. VMs on this network can talk to each other, but that’s it. It’s perfect if you want to isolate a group of VMs for secure testing without any outside interference.

5. **Host-Only Adapter**: Host-Only Adapter creates a direct link between your host machine and your VMs without internet access. The VM can talk to the host and other VMs on the same setting, but it’s fully isolated from the wider network. This is useful for testing things locally or setting up a host-to-VM-only environment.

For this project, we will be using the **NAT Network** setting, this will allow us to have the VMs communicate with one another, while also having access to the Internet.

---

## Download VirtualBox

### Step 1
Navigate to [VirtualBox.org](https://www.virtualbox.org/wiki/Downloads). Select the Host operating system you are currently working with.
![Windows Full Screen Screenshot](https://i.imgur.com/HytutH3.png)
### Step 2
Select all system defaults designated in the installation wizard, unless you would like to customize.
![Windows Full Screen Screenshot](https://i.imgur.com/Vw9VRIU.png)
---

## Host Key
In VirtualBox, the **Host Key** is a special key or combination of keys that allows you to interact with the VirtualBox application itself rather than the guest operating system running inside the virtual machine (VM).

### Key Details about the Host Key:
1. **Default Host Key**: On most systems, the default Host Key is the **Right Ctrl** key. However, this can vary based on your system configuration or preferences.

2. **Purpose of the Host Key**: 
   - **Releasing Keyboard and Mouse Input**: If the VM has captured your mouse or keyboard input, pressing the Host Key releases the input back to the host operating system.
   - **Accessing VirtualBox Features**: You can use Host Key combinations to perform actions like switching to full-screen mode, capturing screenshots, or opening the VirtualBox menu.
To view your current Host Key setting, go to **File → Preferences → Input**, then view the **Host Key Combination**. You can change the Host Key by selecting the box and then hitting the key on the keyboard to specify which key to use.
![Windows Full Screen Screenshot](https://i.imgur.com/8vOoaeO.png)
![Windows Full Screen Screenshot](https://i.imgur.com/vQI7Lyc.png)
---

## Provision A New NAT Network In VirtualBox

### Step 1
Navigate to **File → Tools → Network Manager**. Select **NAT Networks → "Create"**.
![Windows Full Screen Screenshot](https://i.imgur.com/FqrcNic.png)
### Step 2
At the bottom, name the NAT Network **"project-x-network"** and choose an IPv4 prefix. Refer to the Project Overview guide for more detail on IPv4 prefixes. Select **"Apply"** to save changes.
![Windows Full Screen Screenshot](https://i.imgur.com/sxdCQAZ.png)

It will be assumed that each time a new Virtual Machine has been provisioned, the **"project-x-network"** NAT Network will be selected for all VMs.

---

## Download ISOs
### From ISO Provider
Downloading from the ISO provider will not lock in the versions used throughout this project. This will likely not result in any major disruption to the project, but UI changes may occur. The ISOs can be downloaded from the ISO providers.

![Windows Full Screen Screenshot](https://i.imgur.com/MCaHibT.png)
---

## Provision A Virtual Machine

### Step 1
Navigate to **VirtualBox → Machine → New**.

![Windows Full Screen Screenshot](https://i.imgur.com/2rulOzt.png)
### Step 2
Enter a name for the virtual machine. Choose default folder location. Select **Type: Microsoft Windows** and **Version: Windows 2022 (64-bit)**.

### Step 3
Add hardware specifications. A minimum of **4 GBs of RAM (4096 MB)** and **2 CPUs** for every virtual machine, unless explicitly expressed. For Windows: Enable EFI.

![Windows Full Screen Screenshot](https://i.imgur.com/QnJVLUg.png)

Allocate a minimum of **50.00 GB** of Virtual Hard disk space.

![Windows Full Screen Screenshot](https://i.imgur.com/pxYfqIW.png)

Review specifications. Select **Finish**.

### Step 4
Select the newly created virtual machine. Go to **Settings**.

![Windows Full Screen Screenshot](https://i.imgur.com/9y2E44B.png)

### Step 5
Select the **Storage** tab. Click the **Empty** optical drive disk. Then select **Choose a disk file…** Navigate to where your ISO has been downloaded. (By default, it should be in the **Downloads** folder). Click **Open** to open the ISO.

![Windows Full Screen Screenshot](https://i.imgur.com/0i4z20v.png)
### Step 6

![Windows Full Screen Screenshot](https://i.imgur.com/WEsni63.png)

Navigate to the **Network** tab. Select **NAT Network** in the Attached to option. Choose **project-x-network** in the Name option. Select **OK**.
![Windows Full Screen Screenshot](https://i.imgur.com/TVZBsmE.png)

### Step 7
Select the Virtual Machine, then select **Start**.

When the machine provisions, you will see a message related to hitting a key. Hit any letter key on your keyboard to provision into the installation wizard of the operating system.

---

## Take A Snapshot

### Step 1
Go to **VirtualBox**. Select **Virtual Machine**, then select **Take**.
![Windows Full Screen Screenshot](https://i.imgur.com/B1mu6E8.png)

### Step 2
Title the snapshot with something descriptive so you can recall what configurations were made up until this point.
![Windows Full Screen Screenshot](https://i.imgur.com/9gFh4S9.png)
---

## Restore Snapshot
Go to **VirtualBox**. Select **Virtual Machine**. Select which snapshot you want to restore to. Then **Restore**.

---

## Full Screen With VirtualBox Guest Additions

### Windows
1. With a running virtual machine, navigate to the menu bar. Go to **Devices → Insert Guest Additions CD image…**.
2. Navigate to the **File Explorer** application in Windows. Go to **This PC**. Click into the **VirtualBox Guest Additions** program.
3. You should see a few executables (programs). Select the generic **VBoxWindowsAdditions** program.
4. Follow the default installation wizard settings.
5. Choose to **Reboot Now**. Allow the Virtual Machine to restart. You should now be able to make the machine full screen.

### Linux
1. With a running virtual machine, navigate to the menu bar. Go to **Devices → Insert Guest Additions CD image…**.
2. A new CD disk image will appear on the toolbar. Select this.
3. A new file menu will appear. Right-click on the whitespace → Select **Open in Terminal**.
4. A new terminal will appear, type the following, type the user’s password:

```bash
sudo ./VBoxLinuxAdditions.run
