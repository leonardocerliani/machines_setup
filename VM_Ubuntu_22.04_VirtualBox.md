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
`General >> Advanced >> Shared Clipboard: Bidirectional`


## Desktop manager
use xfce4 as default for the VM (gnome gives keypress latency)
`/etc/gdm3/custom.conf <- add DefaultSession=xfce`

If you use ubuntu/gnome, **remove animations** :
`Settings >> Accessibility >> Disable Animations`

## Software to install
- [kinto.sh](kinto.sh) (install using Ubuntu on Xorg)

- [Gogh terminal themes](https://gogh-co.github.io/Gogh/) Novel / Dracula


- `btop` and `htop` : resources monitor
- `nnn` : file manager
- `micro` : terminal text editor `curl http://getmic.ro | bash`
- `docker` : `sudo apt install docker.io`
- `vscode` : text editor
- `atom` + `rmate` : text editor
- `obsidian.md` : markdown editor

## Remote connectivity
- `twingate`
- `x2goclient`

## Initial settings
### Add user(s) to the docker group
`sudo usermod -aG docker $USER`

### Install screenshot tool
from [here](https://extensions.gnome.org/extension/1112/screenshot-tool/)
This requires installing the [GNOME shell integration](https://addons.mozilla.org/en-US/firefox/addon/gnome-shell-integration/?utm_source=addons.mozilla.org&utm_medium=referral&utm_content=search) and the `gnome-screenshot` (using apt).
I then remapped the keybindings to capture an area onto `CMD + 4`.

## Tweaks

### Screen goes blank after a few seconds
Despite setting the option to 15' in the Power Management.
It is suggested [here](https://askubuntu.com/questions/826190/ubuntu-16-04-lts-64bit-screen-goes-black-every-15-seconds) to issue `xset -dpms`

### VirtualBox installation fails due to security restrictions 
In Mac OS (Mojave in my case). To fix this, check [here](https://osxdaily.com/2018/12/31/install-run-virtualbox-macos-install-kernel-fails/)

### Expanding the disk size in Parallels Desktop
See [here](https://kb.parallels.com/en/129758) for instructions


