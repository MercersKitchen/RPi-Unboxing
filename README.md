# RPi-Unboxing
How to Unbox a Raspberry Pi and get it ready for Mercer's Kitchen Projects

**Note**: this document written with GitHub Markup List tool
- Use in paper form or README.md form (see https://github.com/MercersKitchen/Markdown-ReadMe-Documentation for more information)

Preparation
- RPi should be on Ethernet Connection until BIOS and WiFi Configured (note: unboxed settings are Great Britain, not Canadian)
- Notes about Passwords:
  - Saving WiFi Credentials (i.e. user name and password) on a Pi can be looked up, especially if password is not changed
  - All RPi's have same default username and password, published world wide
  - MD5 Hashing is an available method that can be accessed through the Terminal, beyond the scope of this document

Steps
- [] Unbox and install all hardware as indicated
- [] Use an SD Card reader-writer to install Raspbian OS
- [] Download <a href="https://www.raspberrypi.org/downloads/raspbian/">Raspbian OS</a>, accessed 20190530
- [] Check SHA-256, accessed 20190530
- [] Locate the Raspbian OS Installation Documentation, accessed 20190530, for additional software and instructions
- [] Ensure SD Card is empty, ```formatted must be "overwritten"```, see <a href="https://www.sdcard.org/downloads/formatter/">SD Formatter</a>
  - New cards might work with a quick format, error will only show at very end of installation (means you would have to start all over again)
- [] Write the .img file to the SD Card, see Raspberry Pi for latest recommendation (see balenaEtcher-Setup-1.4.9-x64.exe)
- [] RPi complete SD Card installation, see <a href="https://www.raspberrypi.org/documentation/linux/software/apt.md">APT on RPi Documentation</a>, accessed 20190530
- [] Configure ```Boot Settings``` with GUI and follow the prompts
- [] [Optional] Verify configuration in ```X $ sudo raspi-config```
  - All settings were OK, 20190305
  - Note: Verify Expanded Memory: Advanced Options / run Expand memory to entire card, OK 20190305
- [] Update, Upgrade, Reboot, and Clean OS (to most current Linux Packages)
  - Note: Update-Upgrade-Reboot should be completed every time RPi is started
  ```
  X $ sudo apt update
  X $ sudo apt update
  X $ sudo reboot
  X $ sudo apt clean
  ```

  - Note: to make all X-lines sudo, elevate from username to root
  - CAUTION: as superuser shell, no protection exists from mistakes ... so do not make any or do not use this method if you are unsure
  ```
  X $ sudo su
  X $ exit
  ```
- [] Install X11VNC on RPi to use with TightVNC Viewer over Local LAN Connection
  - For TightVNC Viewer Instructions for a Windows OS, see <a href="https://github.com/MercersKitchen/BYOD#tightvnc">Mercer's Kitchen BYOD Repository</a>, and <a href="https://github.com/MercersKitchen/BYOD/tree/master/TightVNC">TightVNC Viewing .exe downloadable</a>
  - Installation of TightVNC Server on RPi (CAUTION: RPi must be secured with unique username and password already)
    - ```X $ sudo apt update``` must be done since reboot, before installing any programs
  ```
  X $ sudo apt install x11vnc
  ```
  - Note: password is needed when not in a secure LAN
- [] Must find RPi IP Address
  - ```X $ ifconfig```, must have head-monitor until IP-Address is known
  - Possible other headless methods: to find IP Address of RPi
    -
      ```
      X $ arp -a | X $ sudo arp -a
      ```
    - Angry IP Scanner
    - SolarWinds IP Tracker
    - My Lan Viewer
    - ```X $ sudo nmap -sS 192.168.1.0/24```
    - Login to the Router and look up the IP Table (specific instructions change depending on the router)
- [] Configure ```X $ ifconfig``` : enabled SSH & VNC using IP Address, record port X11vnc is using
- [] Use PuTTy or CDM.exe to SSH into RPi (perhaps start x11vnc)
  - SSH port is 22
  - Starting X11VNC: ```X $ X11VNC```
- [] Use TightVNC on Viewing Computer, needs socket (and x11vnc to be started) so remember the port number for X11VNC (5900 or 5901)
- [] Test that SSH and TightVNC Works

Note: 
- [] RPi as a WireGuard Server must be left on, IP from Router should be "static" (Look up how to configure Static IP Address)

---

# To Include

Figure out a way to include MD5 Hashing, possible project with Michael (Lilian Osborn)

Look up how to configure Static IP Address on the RPi

Also, look up how to configure a Static IP Address on the DHCP Service on the Router


---
