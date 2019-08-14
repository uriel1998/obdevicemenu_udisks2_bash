# obdevicemenu_udisks2_bash
A bash implementation of obdevicemenu that utilizes udisks2


An Openbox pipe menu for the management of removable media with Udisks

dependecies

udisks2
lsblk


A WORK IN PROGRESS, folks.

obdevicemenu is an Openbox pipe menu that uses udisks to easily mount, unmount or eject removable devices. An extensive configuration file allows desktop notifications about the success or failure of operations, as well as the modification of several commands.

This script does not provide automounting of removable media as there are already many ways to automount. The file managers in GNOME and KDE handle automounting, while udev rules or scripts like Udiskie can be used in other environments.

Notes
Dbus  and consolekit/policykit need to be running. If you aren't using a login manager, put this in ~/.xinitrc:

source /etc/X11/xinit/xinitrc.d/30-dbus
exec ck-launch-session openbox

If it doesn't already exist, create the file "/etc/polkit-1/localauthority/50-local.d/10-udiskie.pkla" with these contents:
```
[Local Users]
Identity=unix-group:storage
Action=org.freedesktop.udisks.*
ResultAny=yes
ResultInactive=no
ResultActive=yes
```
Then put inside the "root-menu" part of ~/.config/openbox/menu.xml something like this:

 <menu id="devices" label="Devices" execute="/usr/bin/obdevicemenu" />
