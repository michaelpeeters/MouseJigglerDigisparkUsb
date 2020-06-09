
# PlatformIO project for MouseJiggler setup of the Digispark USB

original code https://air-gap.com.au/how-to-make-a-mouse-jiggler-with-digispark/

## setup

PlatformIO in VSCode + install Digispark

## troubleshoot PlatformIO on Ubuntu :

### use latest micronucleus on PlatformIO
https://kovo-blog.blogspot.com/2019/01/how-to-upgrade-bootloader-on-digistump.html
```
git clone https://github.com/micronucleus/micronucleus.git
cd micronucleus/commandline/
make
mv ~/.platformio/packages/tool-micronucleus/micronucleus  ~/.platformio/packages/tool-micronucleus/micronucleus.orig
cp micronucleus ~/.platformio/packages/tool-micronucleus/micronucleus
```

### fix the UDEV rules

 http://digistump.com/wiki/digispark/tutorials/linuxtroubleshooting#ubuntu_troubleshooting

/etc/udev/rules.d/49-micronucleus.rules
```
# UDEV Rules for Micronucleus boards including the Digispark.
# This file must be placed at:
#
# /etc/udev/rules.d/49-micronucleus.rules    (preferred location)
#   or
# /lib/udev/rules.d/49-micronucleus.rules    (req'd on some broken systems)
#
# After this file is copied, physically unplug and reconnect the board.
#
SUBSYSTEMS=="usb", ATTRS{idVendor}=="16d0", ATTRS{idProduct}=="0753", MODE:="0666"
KERNEL=="ttyACM*", ATTRS{idVendor}=="16d0", ATTRS{idProduct}=="0753", MODE:="0666", ENV{ID_MM_DEVICE_IGNORE}="1"
#
# If you share your linux system with other users, or just don't like the
# idea of write permission for everybody, you can replace MODE:="0666" with
# OWNER:="yourusername" to create the device owned by you, or with
# GROUP:="somegroupname" and mange access using standard unix groups.
```

reload udev:
```
sudo udevadm control --reload-rules
```
