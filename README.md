# Intel Intel Wi-Fi 6 AX200 (AX200D2WL)

`3a:00.0 Network controller [0280]: Intel Corporation Device [8086:2723] (rev 1a)`

##### Issue:
Wireless doesn't work

##### Fix:
Just upgrade to the latest Linux Kernel, >5.1, and use the latest firmware for the Wireless adapter: https://www.intel.com/content/www/us/en/support/articles/000005511/network-and-i-o/wireless-networking.html 

##### References:
- [Locating Drivers for Intel AX200 Wireless on 5.1 Kernel](https://unix.stackexchange.com/a/532544)
- [Linux Kernel 5.1 Released! How to Install it in Ubuntu](http://ubuntuhandbook.org/index.php/2019/05/linux-kernel-5-1-released-install-in-ubuntu-18-04/)

# Touchpad 

##### Issue:

Tocuhpad doesn't work after suspend

##### Fix:

Create new file `/lib/systemd/system-sleep/fixtouchpad` root:root 755 with this content:

```
#!/bin/sh

case $1/$2 in
  pre/*)
    echo "Going to $2..."
    # Place your pre suspend commands here, or `exit 0` if no pre suspend action required
    modprobe -r i2c_hid
    ;;
  post/*)
    echo "Waking up from $2..."
    # Place your post suspend (resume) commands here, or `exit 0` if no post suspend action required
    sleep 2
    modprobe i2c_hid
    ;;
esac

```

##### References:
- [Touchpad not working after suspending laptop](https://askubuntu.com/a/828920)
- [Zbook G5: Touchpad doesn't work after suspend/resume](https://forums.linuxmint.com/viewtopic.php?t=299541)

