# XPS 9570 OpenSuse Installation Guilde

***Disclaimer:*** *This instruction only apply to tumbleweed if you go for leap version, you must add some repositories first.

## It is quite tricky and complicate, so I will create a shell script later.

### My XPS 9570 Specs
* CPU: Intel® Core™ i7-8750H
* RAM: 16 GB
* HDD: 1 TB
* Video card: NVIDIA® GeForce® GTX 1050 Ti
* Screen: FHD non-touch
* Wi-Fi: Killer 1535
* Battery: 97 Whr

### Before install
You must:
* Burnt ISO onto your USB (>4 GB)
* Disable *Secure Boot* (You can enable it later)
* Enable *Legacy Boot* (Make boot entry do not jump straight in the installation process, you can disable it later)
* Change Sata mode to AHCI (I read something about soft raid in Opensuse artical, but I am not an expert in some kind of partition so let's pick AHCI)

### During installation
#### At the very beginning:
* Boot your usb with OpenSuse to system.
* When the first openSuse Installation menu appears, move hightlight to "Installation" and strike the `e` key
* Move the cursor to the end of a line beginning with `linux` and ending with `splash =silent` and/or `quiet`, append a space and `nomodeset` (9570 have optimus graphic card)
* Striking `F10` or `Ctrl + X`
* If you see a green bar moving, we're in good shape.
#### Installation process:
* You do not need to have internet connection so configure as you like
* You can skip internet configuration in the process.
* **In Installation Settings** which you confirm installation, click `Booting`-Hightlight heading to change your Bootloader type you want to use.
* In Software heading you can change what packages you want to install
#### After installation:
* Reboot your laptop

### Post Installation
* Connect to Wi-Fi and update system: `zypper refresh && zypper update`
* In openSuse TumbleWeed NVIDIA driver is installed in install process but in leap version you need to add repos to install it. ( You can find it [here](https://en.opensuse.org/SDB:NVIDIA_drivers))
* Then we install primer-select in suse by typing in terminal `zypper in suse-prime bbswitch`
* Switch to intel driver 'sudo prime-select intel`
* Restart your laptop `sudo reboot -p' 
* Move hightlight at the top, strike `e`. Delete `nomodeset` option which we typed ealy on
* `Ctrl + x` to boot the system
* After booting to system, type to terminal ` sudo vim /etc/default/grub`
* In line `GRUB_CMDLINE_LINUX_DEFAULT`, delete `nomodeset`. After that this line will look like `GRUB_CMDLINE_LINUX_DEFAULT="splash=silent resume=YOUR/DIRECT/TO/swap quiet mitigations=auto"`
* Press Esc key and type `:wq` to quit vim
* Type `grub2-mkconfig -o /boot/grub2/grub.cfg` to update your bootloader

 **Note** You should use XServer because suse-prime do not support wayland
 
 And now we have fuctional opensuse on Xps 9570. If you find some issues please let me know. 
This is the first time I have installed on my xps 9570 after I messed up with my last distro_Ubuntu.
