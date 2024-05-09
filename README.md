# rtl8852be_bt

## Introduction
This code is for realtek 8852BE bluetooth.  
HRex39 cloned original code from [Linux 5.15 Kernel LTS](https://www.kernel.org/) and changed it a bit.   
It can now support Ubuntu 22.04 LTS(need more test).
I extended the versions with `.1` to able to compile and install with DKMS, and I wrote a `dkms.conf` also.
Any ideas are welcomed, but this is only for Ubuntu 22.04 only, the newer Ubuntu versions should support this BT device out-of-the-box.

## Prerequisites
```
build-essential 
linux-headers
bc
```

## Usage
### 1. Check your Bluetooth Device
```
$ lsusb
$ Bus 003 Device 005: ID 0bda:4853 Realtek Semiconductor Corp. Bluetooth Radio
```

### 2. Clone the repo into the right place with version
```
$ sudo git clone https://github.com/darpakiss/rtl8852be_bt.git /usr/src/rtl8852be_bt-0.8.1
```

### 3. Modify/Add your USB DEVICE in btusb.c
[Modify Here](https://github.com/HRex39/rtl8852be_bt/blob/5.15/btusb.c#L424)  
```
/* Realtek 8852BE Bluetooth devices */
{ USB_DEVICE(0x0bda, 0x4853), .driver_info = BTUSB_REALTEK |
               BTUSB_WIDEBAND_SPEECH },

// USB_DEVICE(0x____ , 0x____) is your ID name which shows in lsusb command
```

### 4. Save and Build
```
#Turn off your Security Boot in BIOS

$ sudo dkms install -m rtl8852be_bt -v 0.8.1 -k "$(uname -r)"
$ sudo reboot
```

## WHAT IS LINUX?
```
WHAT IS LINUX?

  Linux is a clone of the operating system Unix, written from scratch by
  Linus Torvalds with assistance from a loosely-knit team of hackers across
  the Net. It aims towards POSIX and Single UNIX Specification compliance.

  It has all the features you would expect in a modern fully-fledged Unix,
  including true multitasking, virtual memory, shared libraries, demand
  loading, shared copy-on-write executables, proper memory management,
  and multistack networking including IPv4 and IPv6.

  It is distributed under the GNU General Public License - see the
  accompanying COPYING file for more details. 
```
