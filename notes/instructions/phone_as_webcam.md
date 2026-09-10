https://youtu.be/-TZxWqAFouI

```sh
yay -S android-tools
yay -S scrcpy v4l2loopback-dkms

sudo modprobe v4l2loopback
echo "v4l2loopback" | sudo tee -a /etc/modules
scrcpy --v4l2-sink=/dev/video2
scrcpy     --no-window     --v4l2-sink=/dev/video2     --video-source=camera     --camera-size=1920x1080     --camera-fps=60     --camera-id=1     --audio-source=output
```
