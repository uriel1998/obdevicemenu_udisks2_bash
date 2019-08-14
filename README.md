# obdevicemenu_udisks2_bash
An Openbox pipe menu for the management of removable media with Udisks utilizing udisks2

## Contents
 1. [About](#1-about)
 2. [License](#2-license)
 3. [Prerequisites](#3-prerequisites)
 4. [How to use](#4-how-to-use)
 5. [TODO](#5-todo)

***
 
## 1. About

`obdevicemenu` is an Openbox pipe menu that uses udisks to easily mount, 
unmount or eject removable devices. An extensive configuration file allows 
desktop notifications about the success or failure of operations, as well as 
the modification of several commands.

This script does not provide automounting of removable media as there are 
already many ways to automount. The file managers in GNOME and KDE handle 
automounting, while udev rules or scripts like Udiskie can be used in other 
environments.

This script was originally written by 
[Jamie Nguyen](https://bbs.archlinux.org/viewtopic.php?id=114702). The original version 
utilized only udisks which is no longer installable in Debian Buster, so... yeah.

## 2. License

This project is licensed under the GPL3 license. For the full license, see `LICENSE`.


## 3. Prerequisites

 * `openbox` window manager. `openbox` can be found on major Linux distributions.
 * `udisksctl` udisks manager. `udisksctl` can be found on major Linux distributions, often part of a package called something like udisks2.  
 * `lsblk` information utitility. `lsblk` can be found on major Linux distributions.
 * policykit (of your choice) should be running.
 * Optionally, a notification manager like `dunst` or `notify-send`.

## 4. How to use

 * Make the script executable and copy/symlink the script to your choice of directory.
 * Edit the configuration file to your liking. Copy the configuration file to `${HOME}/.config/obdevicemenu/config` 


 * Dbus and consolekit/policykit need to be running. If you aren't using a login manager, put this in `~/.xinitrc`:
``` 
source /etc/X11/xinit/xinitrc.d/30-dbus
exec ck-launch-session openbox

```
 * If it doesn't already exist, create the file `/etc/polkit-1/localauthority/50-local.d/10-udiskie.pkla` with these contents:

```
[Local Users]
Identity=unix-group:storage
Action=org.freedesktop.udisks.*
ResultAny=yes
ResultInactive=no
ResultActive=yes
```

 * Place an entry calling obdevicemenu in your openbox menu, like so:

```
<menu execute="/home/user/bin/obdevicemenu" id="devices" label="devices"/>
```

and the magic should happen. You will be able to mount and unmount various devices.


## 5. Todo

 * Ejection - not intuitively handled by udisks2
 * Additional drive information - again, not udisks2 equivalent
 * Better support/recognition of internal devices
