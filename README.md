# Setting Up a Pi Server
Walk through to setting up a Samba server on Raspberry Pi.

Follow this link to configure and install OS onto your Raspberry Pi SD Card: [BerryBoot](https://www.makeuseof.com/tag/dual-boot-raspberry-pi/).  
Raspbian OS is the recommended choice, you could install another OS if you'd prefer.

Once your Pi is booted up, display and input devices connected, launch the terminal. 

1. We will now update and upgrade our Pi.  
Type the following commands into the terminal:  
`sudo apt-get update`  
Once this process is successful, type:  
`sudo apt-get upgrade`   
Your systems are now up-to-date.

2. This is a troubleshooting step, if you encountered no errors in the previous step, please skip this step.  
If you recieve a dphys swapfile error, while trying to update/upgrade the system:  
A swap space is used when the system RAM is full, so inactive pages on the RAM are moved to the swap space to free up RAM. The swap space is usually located on a hard disk, in this case, the Pi's SD Card.  
This error pertains to swap service. This could've happened because a testing stage version of the kernel might've been installed. These commands would restore the kernel/bootcode to the latest supported versions.  
`sudo apt update`  
`sudo apt install --reinstall raspberrypi-bootloader raspberrypi-kernel`  
Once our kernel is restored, let's disable the swap service. We will be disabling execute permissions, so that the swap service won't restart every time the system reboots:  
`sudo chmod -x /etc/init.d/dphys-swapfile`  
`sudo swapoff -a`  
`sudo rm /var/swap`  
Even with the execute permissions disabled, the symbolic links in runlevels will try to run the dphys swapfile, so we shall remove these symbolic links:  
`sudo update-rc.d -f dphys-swapfile remove`  
Now reboot the system:  
`sudo reboot`  
Now repeat Step 1. This time it should not return any errors. If error persists, it could be an SD Card problem, format, re-install Raspbian and try again.  
If that doesn't work, the SD Card might be, although highly unlikely, corrupted. Try again with another SD Card.

3. Enable SSH through `Preferences> Raspberry Pi Configuration> Interfaces> SSH> Enabled`. SSH is how we can remotely communicate with our Pi from your laptop/PC terminal. 
In the Pi terminal type:  
`hostname -I`  
Note down the IP address (Usually in the form of 192.xxx.xxx.xxx) of your Pi.   
Open the Command Prompt on your PC as administrator and type:  
`ssh pi@192.xxx.xxx.xxx` and click `Enter`  
If prompted whether you want to proceed, type `Y` and click `Enter`
You will be prompted to enter a password, which by default is `raspberry` and click `enter`  
You are now remotely communicating with your Pi.  

4. This is another trouble shooting step. If your previous step was successful, skip this one
