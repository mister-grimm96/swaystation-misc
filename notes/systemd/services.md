## auto-cpufreq

```sh
git clone https://github.com/AdnanHodzic/auto-cpufreq.git
cd auto-cpufreq && sudo ./auto-cpufreq-installer
```

config :

- `sudo nvim /etc/auto-cpufreq.conf`

```
[charger]
governor = performance
energy_performance_preference = performance
energy_perf_bias = performance
platform_profile = performance
enforce_platform_profile = true
turbo = always

[battery]
governor = powersave
turbo = auto
```

---

## zram service

- `sudo pacman -S zram-generator`
- `sudo nvim /etc/systemd/zram-generator.conf`

```
[zram0]
compression-algorithm = zstd
zram-size = ram
swap-priority = 100
fs-type = swap
```

---

## remapping with xremap

- `cargo install xremap --features wlroots`
- `nvim $HOME/.config/xremap/config.yml`

```yml
modmap:
  - name: Numpad to Arrows
    remap:
      KP8: UP
      KP4: LEFT
      KP6: RIGHT
      KP2: DOWN
      KPMINUS: MINUS
```

- `sudo nvim /etc/systemd/system/xremap.service`

```toml
[Unit]
Description=xremap

[Service]
Type=oneshot
KillMode=process
ExecStart=/home/name/.cargo/bin/xremap /home/name/.config/xremap/config.yml
ExecStop=/usr/bin/killall xremap
Restart=on-failure
RestartSec=10

[Install]
WantedBy=default.target
```
