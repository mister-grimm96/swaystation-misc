# important packages for laptop settings

## Brightnessctl

- brightnessctl

the following file must be created to access brightness control in polybar:

```
sudo nvim /etc/udev/rules.d/backlight.rules
ACTION=="add", SUBSYSTEM=="backlight", RUN+="/bin/chgrp video $sys$devpath/brightness", RUN+="/bin/chmod g+w $sys$devpath/brightness"
sudo usermod -aG video $USER
```

## Enable touchpad gestures

- create a file at `/etc/X11/xorg.conf.d/90.touchpad.conf`
- add the following lines :

```
Section "InputClass"
        Identifier "touchpad"
        MatchIsTouchpad "on"
        Driver "libinput"
        Option "Tapping" "on"
EndSection
```

## Set up environment variables

- open `/etc/environment` and add the following lines :

```
QT_QPA_PLATFORMTHEME=gtk3
BROWSER=librewolf
EDITOR=nvim
TERMINAL=footclient
XDG_CURRENT_DESKTOP=sway
XDG_SESSION_DESKTOP=sway
XDG_SESSION_TYPE=wayland
```

## sddm sugar-candy theme

```
$ sudo cp /usr/lib/sddm/sddm.conf.d/default.conf /etc/sddm.conf

$ sudo nvim /etc/sddm.conf

# set the theme to sugar-candy
[Theme]
# Current theme name
Current=sugar-candy
```

## Splash screen : plymouth

```
# check available themes
$ sudo plymouth-set-default-theme -l

# Set a splash theme
$ sudo plymouth-set-default-theme -R solar

$ sudo nvim /etc/mkinitcpio.conf
# add plymouth hook
HOOKS=(base udev plymouth autodetect microcode modconf kms keyboard keymap consolefont block filesystems fsck)
# update:
$ sudo mkinitcpio -p linux
```

## Flags for chromium based borwsers

### files for browsers

- brave-flags.conf
- brave-origin-flags.conf
- chrome-flags.conf
- chromium-flags.conf

```
--ozone-platform=x11
--ignore-gpu-blocklist
--enable-zero-copy
--enable-features=VaapiVideoDecodeLinuxGL
--enable-features=VaapiVideoDecoder,VaapiIgnoreDriverChecks,Vulkan,DefaultANGLEVulkan,VulkanFromANGLE
```

> put them in the .config directory

## image preview with sixel

- libsixel
- imagemagick

## zen browser

- `zen.urlbar.replace-newtab` - false
- `zen.view.experimental-no-window-controls` - true

---

## xfce minimal install:

```sh
xorg_packages=(
xfce4-session
xfce4-panel
xfwm4
xfce4-settings
xfce4-pulseaudio-plugin
xfce4-cpufreq-plugin
xcec4-sensors-plugin
xorg
xorg-server
lxappearance
xsel
xorg-xrandr
xdotool
feh
)

for package in "$xorg_packages"; do
  if pacman -Qq "$package" &>/dev/null; then
    echo "$package already installed."
  else
    echo "Installing $package..."
    sudo pacman -S --noconfirm "$package"
  fi
done
```
