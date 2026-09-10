## remove plymouth

1. `sudo pacman -Rns plymouth cachyos-plymouth-bootanimation cachyos-plymouth-theme`
2. `sudo nvim /etc/mkinitcpio.conf`
3. remove `plymouth` from the `Hooks`
4. `sudo mkinitcpio -P`

## remove passwrord encryption echo from sdboot-manager

1. sudo `/etc/sdboot-manage.conf`
2. remove `quite splash` add : `rd.luks.options=password-echo=no`
3. `sudo sdboot-manage gen`
