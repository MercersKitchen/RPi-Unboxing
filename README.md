# RPi-Unboxing
How to Unbox a Raspberry Pi and get it ready for Mercer's Kitchen Projects

REMINDER: organize your SD Cards
- Give them to Mr. Mercer, labeled inside your USB SD Reader-Writer and he will return it the next lesson

**Note**: this document written with GitHub Markup List tool
- Use in paper form or README.md form (see https://github.com/MercersKitchen/Markdown-ReadMe-Documentation for more information)

Preparation
- RPi should be on Ethernet Connection until BIOS and WiFi Configured (note: unboxed settings are Great Britain, not Canadian)
- WiFi is never preferred for stability and security reasons

General Hardware Setup
- Full setup, then headless
- Ensured, Putty, TightVNC, and X11VNC
- Headless is done with outside IP (not 169.254.xxx.xxx), bridged connection through Network Connections

- Notes about Passwords:
  - Saving WiFi Credentials (i.e. user name and password) on a Pi can be looked up, especially if password is not changed
  - All RPi's have same default username and password, published world wide
  - MD5 Hashing is an available method that can be accessed through the Terminal, beyond the scope of this document

Steps
- [] Unbox and install all hardware as indicated
- [] Use an SD Card reader-writer to install Raspbian OS (have this ready)
- [] Download <a href="https://www.raspberrypi.org/downloads/raspbian/">Raspbian OS</a>, accessed 20190530
  - Making the process faster: download <a href="https://www.freedownloadmanager.org/">"Free Download Manager"</a>, accessed 20190605
  - MercersKitchen used fdm5_x64_setup.exe
  - Use it to download Raspbian OS
  - Able to use Torrent
  - Do not use to "Catch all downloads from Chrome"
  - Drag and Drop URL to Download: RightClick in Webpage on Download Link, copy URL
  - In FDM / Click + / URL should populate from Clipboard / Change Folder / Start Download
  - Save the download to a parent folder on the CDrive (makes imaging the SD Card easier due to write distances)
- [] Check SHA-256, accessed 20190605
  - See instructions from https://github.com/MercersKitchen/BYOD#md5-checksum-file-integrity
  - Use CMD: ```c:```, ```cd```
  - Copy Command and change the ```FILENAME```
  - Verify the Checksum Output in Notepad: website answer with downloaded answer
- [] Locate the Raspbian OS Installation Documentation, <a href="https://www.raspberrypi.org/documentation/installation/installing-images/">accessed 20190606</a>, for additional software and instructions
- [] Ensure SD Card is empty, ```formatted must be "overwritten"```, see <a href="https://www.sdcard.org/downloads/formatter/">SD Formatter</a>
  - New cards might work with a quick format, error will only show at very end of installation (means you would have to start all over again)
  - Best Practice: use the overwrite feature
  - CAUTION: ensure the drive letter is correct before formatting (use File Explorer to verify)
  - Note: if SD Formatter doesn't work, format the SD Card to FAT23 (4Gb max file size) or NTFS (larger file size available in Windows 10)
- [] Write the ```.img``` file to the SD Card, see Raspberry Pi for latest recommendation (see balenaEtcher-Setup-1.4.9-x64.exe (includes great installer), <a href="https://www.balena.io/etcher/">accessed 20190606</a>)
  - Instructions for are part of the design for Etcher, a huge positive :), also has a Github Repo for those wanting to contribute
  - Optional: Win32DiskImager, <a href="https://sourceforge.net/projects/win32diskimager/">accessed 20190606</a>
    - Instructions are <a href="https://raspberry-projects.com/pi/pi-operating-systems/win32diskimager">here, accessed 20190606</a>
- **Lesson Interruption**: if the lesson is interrupted, put the SD Card into the card reader and label the Card Reader with the student's name, return everything the next lesson with a RPi to connect locally
- [] RPi complete SD Card installation, see <a href="https://www.raspberrypi.org/documentation/linux/software/apt.md">APT on RPi Documentation</a>, accessed 20190530
- [] Configure ```Boot Settings``` with GUI and follow the prompts
  - Set the following, (as of 20190607)
    - Country: Canada
    - Language: Canadian English
    - Timezone: Edmonton
    - Use US Keyboard
  - Click NEXT
  - OPTIONAL: Change Password (Caution: security issue), "Hide Characters" means password HASHED
  - Setup Screen: ensure geometry is OK
  - WiFi: skip
  - Update Software: skip (until we have headless network access)
  - CLICK Restart
  - CLICK Raspberry (Top Right Corner / Preferences / Raspberry Pi Configuration)
  - Interfaces TAB / Enable SSH, Enable VNC
  - Localization TAB: ensure all are set correctly
- [] Bridge Connections on Laptop to RPi (requires Ethernet cable)
  - WINDOWS Key / WiFi / Change Adapter Options
  - Network Connections / Bridge Ethernet with WiFI (use Ctrl Key & RightClick)
  - Verify IPv4 is bridged through eth0 (Ethernet port): ```X $ ifconfig```
    - Not Bridged Address: 169.254.XXX.XXX, 10.XXX.XXX.XXX, or 127.0.0.XXX,
    - Bridged Address: anything other than or
  - OPEN Terminal, update OS Reading of Package Dates (must be done before installation of any software or upgrade)
    - ```X $ sudo apt update```
  - Install X11VNC Server: ```X $ sudo apt install x11vnc``` (Note: password is needed when not in a secure LAN)
  - Ensure software is installed on the Laptop: PuTTy & TightVNC
    - PuTTy, <a href="https://www.putty.org/">accessed 20190607</a>, standard installation
    - TightVNC, <a href="https://www.tightvnc.com/download.php">accessed 20190607</a>, CAUTION: ensure Server feature is unavailable on the laptop (Installation / Custom Install / X-out the Server)
  - Execute PuTTy on Laptop: enter the Socket and connect (will need the Username and Password of the RPi)
    - In the Terminal, execute X11VNC (```X $ x11vnc```)
    - Record the port number given
  - Execute TightVNC on the Laptop: enter the Socket and connect (will need the port number given by X11VNC through the Terminal of PuTTy using the SSH Protocol)
    - remember the port number for X11VNC (5900 or 5901)

**You now have a headless connection with the Raspberry Pi using a Virtual Network**
- Alternate method to TightVNC & X11VNC is Chrome Extension "Real VNC" & Real VNC (in Raspberry Pi Configuration)

- [] [Optional] Verify configuration in ```X $ sudo raspi-config```
  - All settings were OK, 20190305
  - Note: Verify Expanded Memory: Advanced Options / run Expand memory to entire card, OK 20190305

- [] Update, Upgrade, Reboot, and Clean OS (to most current Linux Packages)
  - Note: Update-Upgrade-Reboot should be completed every time RPi is started
  ```
  X $ sudo apt update
  X $ sudo apt upgrade
  X $ sudo reboot
  X $ sudo apt clean
  ```

  - Note: to make all X-lines sudo, elevate from username to root
  - CAUTION: as superuser shell, no protection exists from mistakes ... so do not make any or do not use this method if you are unsure
  ```
  X $ sudo su
  X $ exit
  ```
  - Cleaner output
  - Note: typing `sudo` when already at root does nothing, redundant
- [] Install X11VNC on RPi to use with TightVNC Viewer over Local LAN Connection
  - For TightVNC Viewer Instructions for a Windows OS, see <a href="https://github.com/MercersKitchen/BYOD#tightvnc">Mercer's Kitchen BYOD Repository</a>, and <a href="https://github.com/MercersKitchen/BYOD/tree/master/TightVNC">TightVNC Viewing .exe downloadable</a>
- Possible other headless methods: to find IP Address of RPi
  - Using ARP Command on Windows Machine: ```X $ arp -a | X $ sudo arp -a```
  - Angry IP Scanner
  - SolarWinds IP Tracker
  - My Lan Viewer
  - ```X $ sudo nmap -sS 192.168.1.0/24```
  - Login to the Router and look up the IP Table (specific instructions change depending on the router)

Note:
- [] RPi as a WireGuard Server must be left on, IP from Router should be "static" (Look up how to configure Static IP Address), DO NOT use any DHCP Service (should be turned off on the Router and RPi)

---

WireGuard or Router Application Additional Step: Enabling RPi IPv4 Forwarding

```
pi@raspberrypi:~ $ sysctl net.ipv4.ip_forward
```

```
Return: net.ipv4.ip_forward = 1
```

If you did that then routing on the pi is enabled so that's good.

If you get ```net.ipv4.ip_forward = 0```,
please manually edit ```X $ sudo nano /etc/sysctl.conf``` and add ```net.ipv4.ip_forward = 1```
- comment out `=0` line

# Final Reminder
Remember to DELETE your Bridged Connection before you shut down your laptop
- Continuing a bridged connection will cause issues the next time you start your laptop and try to use WiFi

---

# To Include

Figure out a way to include MD5 Hashing, possible project with Michael (Lilian Osborn)

Look up how to configure Static IP Address on the RPi

Also, look up how to configure a Static IP Address on the DHCP Service on the Router

Alternate way of Discovering IP Addresses for Locally Connected Machines
- https://hobbyistsoftware.com/bonjourbrowser
- Needs to be tested

---
