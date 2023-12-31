# Ubuntu 22.04 on Imac 13,2 Brightness control.

There is a well known problems about adjusting display brightness in Ubuntu. 
I tried several options described in askubuntu.com, and the followings are those which worked

## Modify `/etc/default/grub`
[link](https://askubuntu.com/questions/1295423/ubuntu-20-04-on-imac-mid-2011-cant-adjust-brightness/1478635#1478635)

```bash
sudo nano /etc/default/grub

# replace this line
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"

# with this
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash pcie_aspm=force acpi_backlight=native"

# then
sudo update-grub

# and then reboot
sudo reboot
```

## Install `brightness-control`
The modification above provided an acceptable default brightness level, however it still didn't get me the possibility of using the brightness adjust keys on the keyboard.

On a [popular forum](https://community.frame.work/t/responded-ubuntu-22-brightness-keys-not-working/22460/23)  it is recommended to blacklist the hid_sensor_hub, either my adding a directive to the `/etc/default/grub`

```bash
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash pcie_aspm=force acpi_backlight=vendor module_blacklist=hid_sensor_hub"
```

or by writing a new file `/etc/modprobe.d/framework-als-blacklist.conf` containing:

```
blacklist hid-sensor-hub
```

Neither of these worked for me. On a [debugpoint.com link](https://www.debugpoint.com/2-ways-fix-laptop-brightness-problem-ubuntu-linux/) I found out that it is possible to install [`brightness-controller`](https://github.com/lordamit/Brightness)

This does the job, but it means having this X window open all the time (no toolbar icon). Still no functionality on the brightness keys.

## Install RedShift
[Redshift](http://jonls.dk/redshift/) is similar to Flux, and can be installed from the Ubuntu snap sw installer.








