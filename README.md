# Resolving Yersinia GUI Issue on Kali Linux

## Problem Statement
Encountering difficulties while attempting to utilize Yersinia's graphical user interface (GUI) on Kali Linux can be quite frustrating. Users may stumble upon the following error message:

```
Hmmm... it seems that you don't have gtk support or Yersinia
has been configured with --disable-gtk option...
Go and get it!!
```

Such issues hinder the seamless execution of network security tests and analysis.

## Environment
- **Operating System:** Kali GNU/Linux Rolling
- **Release:** 2024.1
  
```
┌──(kali㉿kali)-[~]
└─$ uname -a
Linux kali 6.6.15-amd64 #1 SMP PREEMPT_DYNAMIC Kali 6.6.15-2kali1 (2024-04-09) x86_64 GNU/Linux
┌──(kali㉿kali)-[~]
└─$ lsb_release -a
Distributor ID: Kali
Description:    Kali GNU/Linux Rolling
Release:        2024.1
Codename:       kali-rolling

```

## Solution Overview
After facing this roadblock and scouring the internet for solutions in vain, it became apparent that the root cause might lie within the installation process or a potential bug. Here's a concise breakdown of how I tackled the problem:

### Step 1: Uninstall Existing Yersinia Package
```bash
apt remove --auto-remove yersinia
apt purge --auto-remove yersinia
```

### Step 2: Clone Yersinia Repository
```bash
git clone https://github.com/tomac/yersinia /opt/yersinia
```

### Step 3: Install Necessary Dependencies
```bash
apt install autoconf libgtk-3-dev libnet1-dev libgtk2.0-dev libpcap-dev -y
```
(NOTE: Ensure libpcap-dev is installed to prevent compilation errors.)

### Step 4: Compile Yersinia
```bash
cd /opt/yersinia
./autogen.sh
./configure --with-gtk
make
make install
```

### Step 5: Test Yersinia GUI
```bash
yersinia -G
```
The GUI should now launch smoothly without encountering the previous error.
