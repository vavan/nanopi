# nanopi
Scripts and settings for "NanoPi 2 Fire" board

#
 cat /etc/hosts
127.0.0.1       localhost
127.0.1.1       NanoPi2


 cat init_reset.sh
#!/bin/bash

#Turn off hardbeat LED
echo none > /sys/class/leds/led1/trigger
echo 0 > /sys/class/leds/led1/brightness

#Enable button gpio
if [ ! -d /sys/class/gpio/gpio71 ]; then
    echo 71 > /sys/class/gpio/export
fi

#Run servise
./reboot_on_btn.py


cat /etc/init.d/button
#!/bin/bash
### BEGIN INIT INFO
# Provides:          button
# Required-Start:    hostname $local_fs
# Required-Stop:
# Should-Start:
# Default-Start:     2 3 4 5
# Default-Stop:
# Short-Description: Create btn
# Description:       /etc/bu
### END INIT INFO


#Turn off hardbeat LED
echo none > /sys/class/leds/led1/trigger
echo 0 > /sys/class/leds/led1/brightness

#Enable button gpio
if [ ! -d /sys/class/gpio/gpio71 ]; then
    echo 71 > /sys/class/gpio/export
fi

#Run servise
echo RESTART >> /home/fa/btn.log
/home/fa/reboot_on_btn.py >> /home/fa/btn.log 2>&1


chmod +x /etc/init.d/button
sudo update-rc.d button defaults

sudo apt-get update && apt-get install openjdk-7-jdk iperf

-- Runlevel 3
systemctl set-default multi-user.target


sudo systemctl disable avahi-daemon.service
sudo systemctl disable avahi-dnsconfd.service
sudo systemctl disable bluetooth.service
sudo systemctl disable vsftpd.service
sudo systemctl disable lightdm.service
sudo systemctl disable ModemManager.service
sudo update-rc.d tightvncserver disable
sudo update-rc.d lcd4linux disable
sudo update-rc.d gpsd disable
sudo update-rc.d isc-dhcp-server disable

# OpenCV 3.2 on raspberry
http://www.pyimagesearch.com/2016/04/18/install-guide-raspberry-pi-3-raspbian-jessie-opencv-3/

# Access to video device (camera, v4l2) 
#  Allows access to camera by for example gstreamer for non root users
#  To figure out the required group do ls -la /dev/<device>
usermod -a -G video vova

