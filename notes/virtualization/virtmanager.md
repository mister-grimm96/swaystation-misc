# virt manager

```sh
sudo pacman -Syyu qemu virt-manager libvirt dnsmasq ebtables iptables-nft
sudo systemctl enable libvirtd
sudo usermod -aG libvirt grimm
sudo usermod -aG kvm grimm
```

```sh
sudo virsh net-list --all
sudo virsh net-autostart default
sudo virsh net-start default
```
