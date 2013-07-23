ralink-driver-3562
==================

Ralink driver 3562 for my HP Pavilion P7-1447C Desktop

Instructions (from http://rricketts.com/installing-ralink-rt3290-wireless-drivers-in-ubuntu-12-04/)
 
1. Check your wireless controller hardware


    lspci | grep Network
    

 You should get the following output
 

    Network controller: Ralink corp. Device 3290
    
    
 If so, you will need to install Ralink driver 3562.

2. Download the driver source from the Ralink website, my local mirror (This Git Repo)


    http://www.ralinktech.com/en/04_support/support.php

3. Extract the folder (DPO_RT3562_3592_3062_LinuxSTA_V2.4.1.1_20101217) to your home directory.
4. Open DPO_RT…/os/linux/config.mk
5. Make the following changes:


    Change line 12 to read HAS_WPA_SUPPLICANT=y
    Change line 15 to read HAS_NATIVE_WPA_SUPPLICANT=y
    

6. Open a terminal


    cd DPO_RT3562_3592_3062_LinuxSTA_V2.4.1.1_20101217
    
7. sudo make
8. Install the driver.


    sudo make install
    
9. Next you need to blacklist the conflicting wireless drivers


    sudo gedit /etc/modprobe.d/blacklist.conf
    Add the following lines:
     Wireless drivers conflicting with rt3562sta
    blacklist rt2800pci
    blacklist rt2x00pci
    
10. Tell linux to load the correct module on boot


    sudo gedit /etc/modules
    Append the following line:
    rt3290sta
    
11. Update the changes


    sudo update-initramfs -u
    
12. Restart your system. You should see a list of available networks in the network manager next time it boots.
