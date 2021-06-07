# Thinkpad-X201-Hackintosh-Catalina

![Thinkpad X201 i7 Catalina OS hackintosh](/Thinkpad-X201-i7-Catalina-OS-hackintosh.JPG)

I have successfully installed Catalina on my ThinkPad X201. Previously I was running High Sierra, Catalina was around the same amount of work to get running, but the Graphics are much better even without metal support. For High Sierra, I had to inject drivers for the graphics card to get things to render, but there would still be artifacting and glitches. Catalina graphics runs perfect on the X201 with full QE/CI acceleration thanks to ASentientBot's kext patches and dosdude1 Catalina patcher.

I have my machine set to dual boot with Windows 7 on a partitioned SSD. The X201 does not have UEFI support, so the SMB partitions are all handled by clover installed to the main drive.

## Spec ##

- Intel® Core™ I7 processor I7-640LM (2.13 GHz) with dual-core
- High Definition (HD) Audio
- Conexant 20585 codec
- Volume up, down, and mute buttons
- Microphone input jack
- Headphone jack

## Wifi ##

You can use built in Intel Wifi card with AirportItlwm.kext (included)

The OEM wifi card will not work in Windows 7. I first upgraded to an Atheros AR9285 which worked natively in both Windows and OS, but it was noticably slower and lack of 5ghz support. I then upgraded to a BroadCom BCM94360HMB which is lighting fast! For Windows, you need to install the Asus AW-CMB160H drivers for it to work, it is not plug and play in Windows. For the antenna connectors, this card uses the new IPEX 4 smaller connectors. If you want to use the built in Thinkpad X201 antennas, you can fit IPEX-4 Female to IPEX-1 adaptors. There's a third antenna too which I fitted a simple IPEX 4 aerial although this is not necessary. I highly recommend the BroadCom AW-CB160 BCM94360HMB it's a very impressive wifi card, and with the SSD installed it's now a very quick machine.

## Working ##

- Upgrades successfully to Catalina 10.15.7
- Volume control buttons
- Built in Bluetooth
- Brightness controls & all keyboard shortcuts
- Sound & Mic
- Webcam
- Bluetooth

## Not yet working: ##

Sleep - working on this! It's very fast to just shut down and boot back up again with the SSD. I can either get it to sleep but the screen doesn't turn off. I have tried the darkwake options but I need to do further investigation.

## Screen resolution ##

There are a couple of different screen resolutions for the thinkpads, mine is set to ~1440x900~ - update, I now have the 1280x800 resolution this is set in the config.plist (or edit with Clover Configurator).

## Instructions ##

1) Download the repo
2) Open config.plist in Clover Configurator. 
3) Set your SMBIOS to MacbookPro 9,2 and generate new UUID/Motherboard ID/System ID/Serials etc.

I will add more instructions to this repo if anyone finds this useful? Does anyone need dual boot instructions for Catalina and Windows 7 - that was quite tricky to get working!

## Installation and enabling QE/CI graphics acceleration ##

1) Use dosdude's Catalina Patcher app for creating bootable usb installer with post install patches (rolling back deprecated graphics kexts, OpenGL frameworks, platform patch, etc)
2) Install OS
3) After OS is installed, run usb installer to apply post install patches (kext, frameworks).
    * Select custom patches selection - for MacBookPro6,1 (which similar to x201 has arrandale CPU/GPU)
    * Select only "Legacy Video Card Patch" and "SIP Disabler Patch"
4) After patches installation (but before reboot), select "Force Cache Rebuild".
    * Important note: If you don't select "Force Cache Rebuild", system will reboot automatically after 10s.
5) Remove entry Devices->FakeID->IntelGfx 0x12345678
6) Boot MacOS, full QE/CI acceleration should working.

Inspired by Badruzeus post on [insanelymac](https://www.insanelymac.com/forum/topic/286092-guide-1st-generation-intel-hd-graphics-qeci/?do=findComment&comment=2732732)

<img src="Thinkpad-X201-i7-Catalina-OS-Arrandale-Acceleration.jpg" alt="Thinkpad-X201-i7-Catalina-OS-Arrandale-Acceleration" height="60%" width="60%">

## Important ##

Kexts can be updated, but don't update VooDooPS2Controller. If you update this, the central red ThinkPad mouse button is no longer supported. Touch features all work, two finger scrolling etc.