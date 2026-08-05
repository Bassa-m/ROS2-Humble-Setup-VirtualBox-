
# Setting Up ROS 2 Humble Environment - Troubleshooting & Migration

This repository documents the steps, obstacles, and alternative solutions encountered while setting up the **ROS 2 Humble** development environment.

## 📌 Project Overview
* **Target OS:** Ubuntu 22.04.5 LTS (Jammy Jellyfish)
* **Target Framework:** ROS 2 Humble Hawksbill
* **Virtualization Tool:** Oracle VM VirtualBox

---

## 🛠️ Troubleshooting: The Windows WSL2 Obstacle

1. **Initial Approach (WSL2):**
   * Attempted to set up the environment using Windows Subsystem for Linux (WSL2) following standard guidelines.
   * Encountered critical Windows component store corruption issues preventing the activation of necessary virtualization features.

2. **Error Encountered:**
   * **Error Code:** `Error: 14098 - The component store has been corrupted`
   * **Root Cause:** Internal OS package/component store corruption within Windows, preventing the successful installation/activation of `VirtualMachinePlatform` and WSL optional features.

3. **Solution & Pivot to VirtualBox:**
   * Decided to bypass the underlying Windows system file corruption by utilizing **Oracle VM VirtualBox** to run Ubuntu 22.04.5 LTS as a fully isolated virtual machine.

---

## 🚀 ROS 2 Humble Installation Steps (Inside Ubuntu 22.04)

Once Ubuntu 22.04 is successfully running inside VirtualBox, open your Ubuntu terminal and execute the following steps:

### 1. Update Core System Packages
Update the system to ensure you have the latest packages:
```bash
sudo apt update && sudo apt upgrade -y

```
### 2. Setup Repositories & Keys
Install the required utility tools and enable the universe repository:
```bash
sudo apt install software-properties-common curl -y
sudo add-apt-repository universe -y

```
Add the official ROS 2 key to ensure package security:
```bash
sudo curl -sSL [https://raw.githubusercontent.com/ros/rosdistro/master/ros.key](https://raw.githubusercontent.com/ros/rosdistro/master/ros.key) -o /usr/share/keyrings/ros-archive-keyring.gpg

```
Add the official repository to your system's sources list:
```bash
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] [http://packages.ros.org/ros2/ubuntu](http://packages.ros.org/ros2/ubuntu) jammy main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null

```
### 3. Install ROS 2 Humble Package
Update the apt repository cache, then begin installing the full (Desktop) version:
```bash
sudo apt update
sudo apt install ros-humble-desktop -y

```
### 4. Permanent Environment Setup
To make ROS 2 commands automatically available every time you open a new terminal, add the setup script to your .bashrc file:
```bash
echo "source /opt/ros/humble/setup.bash" >> ~/.bashrc
source ~/.bashrc

```
### 5. Verification
To ensure the system recognizes the ROS environment variables, run the following command:
```bash
printenv ROS_DISTRO

```
**Expected Output:** The system should print the word humble, confirming that the installation was successful and the workspace is ready for development.
```

```
