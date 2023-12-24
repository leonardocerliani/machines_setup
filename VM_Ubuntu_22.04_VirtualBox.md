# Ubuntu 22.04 LTS on VirtualBox 

## VM settings
- 16GB RAM
- 48MB Video Memory
- 3 cores
- Use VMSVGA and Enable 3D acceleration

### Enable dynamic change of display size
`Device >> Install Guest Additions CD`

Sometimes the autorun does not work. Check out these videos: [1](https://www.youtube.com/watch?v=ULSFaGmIaUo),[2](https://www.youtube.com/watch?v=KfSxpxKLjWU)

### Enable bidirectional cp/paste
General >> Advanced >> Shared Clipboard: Bidirectional


## Desktop manager
use xfce4 as default for the VM (gnome gives keypress latency)
`/etc/gdm3/custom.conf <- add DefaultSession=xfce`

If you use ubuntu/gnome, **remove animations** :
`Settings >> Accessibility >> Disable Animations`

## Software to install
- [kinto.sh](kinto.sh) (install using Ubuntu on Xorg)

- [Gogh terminal themes](https://gogh-co.github.io/Gogh/) Novel / Dracula



- htop
- btop
- micro `curl http://getmic.ro | bash`
- `sudo apt install docker.io`
- vscode
- twingate
- x2goclient

