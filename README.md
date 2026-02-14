Adaptador WiFi 6 Realtek RTL8832CU (AX5400) en Ubuntu 22.04
This guide detail how to configure the USB WiFi 6 antenna that use RTL8832CU Chipset. 
which usually present an initial "virtual CD-ROM" mode in Linux.(Or something similar to a Windows driver installer. In any case, it's "resettable with the antenna button.")


## 1- REQUIREMENTS

  * Update
  * Disable Secure Boot in BIOS/UEFI

@@ 2- Identificate and change mode

  >lsusb 

  If you see 0bda:1a2b: It's in CD-ROM mode.
  If you see 0bda:c832: It's ready for the driver.

  U need to force the change, u can do it pressing the antenna button or using command line.
 
    > sudo eject /dev/sr0 # OR /dev/sr1 as appropriate 
  
## 3- Install Drivers
  We will use the morrownr repository, which is the most up-to-date for the 8852cu/8832cu series and modern kernels (6.8+).

  > # Clone the specific repository
  > git clone https://github.com/morrownr/rtl8852cu-20240510.git
  > # Enter the directory
  > cd rtl8852cu-20240510
  > # Run the automated installation script
  > sudo ./install-driver.sh

  During installation:
  When prompted to edit the driver options, select n (No).
  When finished, select y to restart the system.

## 4- Post-Installation Configuration
  After restarting, the system may attempt to use both the internal and USB adapters, causing connection conflicts.

  Disabling Internal Wi-Fi (Optional but Recommended)
    If your internal interface is wlo1 and the new one is wlx..., disable the internal interface to avoid interference:

     > sudo ip link set wlo1 down

  Network Management
    If it doesn't ask for a password or doesn't connect to known networks:
    1º. Go to Wi-Fi settings and just "Forget network."
    2º. Reconnect, specifically selecting the USB adapter interface.

## 5- Verify 
  To confirm, verify the comand.
  > iwconfig
  Look for the line that mentions IEEE 802.11AC or 802.11AX in the new interface.

## 6. Have Fun... 
  Im testing the antenna...
