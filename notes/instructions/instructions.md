# cmus new package list

- `sudo pacman -S cmus faad2 libao libcddb libiconv libmp4v2 libmpcdec opusfile wavpack`

---

### Drivers:

```sh
# amd
xf86-video-amdgpu
xf86-video-ati
amd-ucode
amdvlk

# intel
intel-media-driver
vulkan-intel
intel-gmmlib
```

# Some notes and commands

## set thems and icons for flatpak apps

check theme and icon

set theme and icon

```
sudo flatpak override --system --reset
sudo flatpak override --filesystem=$HOME/.themes/
sudo flatpak override --filesystem=$HOME/.icons/
sudo flatpak override --env=GTK_THEME=Orchis-Grey-Dark-Compact
sudo flatpak override --env=ICON_THEME=Papirus
```

flatpak global override configs are in : `cd /var/lib/flatpak/overrides`

---

## Add fav Bookmarks in file managers

- `nvim ~/.config/gtk-3.0/bookmarks`
- `nvim ~/.config/gtk-4.0/bookmarks`

```
file:///home/grimm/Desktop Desktop
file:///home/username/Documents Documents
file:///home/username/Downloads Downloads
file:///home/username/Projects Projects
file:///home/username/Pictures Pictures
file:///home/username/Pictures/screenshots screenshots
file:///home/username/Pictures/memes memes
file:///home/username/Videos Videos
file:///home/username/Videos/tutorials tutorials
file:///home/username/Videos/movies movies
file:///home/username/Videos/screenrecords screenrecords
```

---

### Ran into an issue related to systemd `a failed ret 0x0`

```
$ sudo nvim /etc/mkinitcpio.conf
# pass parameter in `modules=()`
$ modules = (amdgpu)
$ sudo mkinitcpio -p linux
```

## always youtube theatre mode

- go to youtube.com
- run the following code in the console

```
document.cookie = 'wide=1; expires='+new Date('3099').toUTCString()+'; path=/';
```

## some weird shit happened with xdg-desktop-portal and screensharing

- fixed by the new systemd config, for other window managers comment these lines :

- `sudo nvim /usr/lib/systemd/user/xdg-desktop-portal.service`

```
PartOf=graphical-session.target
Requisite=graphical-session.target
After=graphical-session.target
```

## issue : https://github.com/flatpak/xdg-desktop-portal/issues/1983

User-level workaround (no package patch needed) — for anyone on a DE that doesn't activate graphical-session.target (Cinnamon/MATE/Xfce/etc.) who can't or doesn't want to rebuild the package:

Note that a systemd drop-in does not work here — dependency directives like Requisite= merge across fragments and cannot be reset from a drop-in, so Requisite= in an override.conf is silently ignored. You need a full unit override instead.

Create ~/.config/systemd/user/xdg-desktop-portal.service (user units take precedence over /usr/lib/systemd/user/):

```
[Unit]
Description=Portal service
PartOf=graphical-session.target
Requires=dbus.service
After=dbus.service
After=graphical-session.target

[Service]
Type=dbus
BusName=org.freedesktop.portal.Desktop
ExecStart=/usr/lib/xdg-desktop-portal
Slice=session.slice
```

Then systemctl --user daemon-reload && systemctl --user start xdg-desktop-portal. This is the same dependency change as Ubuntu's allow-no-graphical-session-target.patch, applied per-user. Adjust ExecStart to /usr/libexec/xdg-desktop-portal on distros that use libexec. Remember to delete the override once your distro patches the package or your DE activates the target.
