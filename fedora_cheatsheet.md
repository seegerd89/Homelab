<img src="https://cdn.svgporn.com/logos/fedora.svg" width="30%" align="right" />

<h1>Fedora CheatSheet</h1>

- [Packages](#packages)
  - [RPM Fusion](#rpm-fusion)
  - [DNF](#dnf)
  - [Flatpak](#flatpak)
- [Multimedia codecs](#multimedia-codecs)
- [Drivers](#drivers)
- [Terminal](#terminal)
  - [Fish Shell](#fish-shell)
  - [Extend inotify](#extend-inotify)
- [Development](#development)
  - [Python](#python)
  - [Node.JS](#nodejs)
  - [PHP](#php)
  - [JetBrains Toolbox](#jetbrains-toolbox)
  - [Visual Studio Code](#visual-studio-code)
  - [Sublime Apps](#sublime-apps)
- [Wireguard VPN](#wireguard-vpn)
  - [Server](#server)
  - [Client (Fedora)](#client-fedora)
- [Containerization](#containerization)
  - [Docker](#docker)
  - [Docksal](#docksal)
- [Desktop](#desktop)
  - [GTK Themes / Icons](#gtk-themes--icons)
  - [Google Fonts](#google-fonts)
  - [Gnome](#gnome)
    - [Gnome Extensions](#gnome-extensions)
- [Tweaks](#tweaks)
  - [Alsamixer save configuration](#alsamixer-save-configuration)
  - [User Dirs in Synology Drive](#user-dirs-in-synology-drive)
  - [NFS Shares](#nfs-shares)
  - [SWAP](#swap)
  - [Boot into last booted grub record](#boot-into-last-booted-grub-record)

---

## Packages

### [RPM Fusion](https://rpmfusion.org/)

> RPM Fusion provides software that the Fedora Project or Red Hat doesn't want to ship. That software is provided as precompiled RPMs for all current Fedora versions and current Red Hat Enterprise Linux or clones versions.


```bash
sudo dnf install -y \
  "https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm" \
  "https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm"
```

### DNF

#### DNF Packages

```bash
APPS=(
  neofetch            # Shows Linux System Information with Distribution Logo
 
  libreoffice

  ffmpeg           # Universal media transcoder tool
  flameshot        # Powerful and simple to use screenshot software
  vlc
) && sudo dnf install -y ${APPS[*]} 
```

<img src="https://upload.wikimedia.org/wikipedia/commons/1/1a/Flatpak_logo.png" width="17%" align="right" />

### Flatpak

> Flatpak is a tool for managing applications and the runtimes they use. In the Flatpak model, applications can be built and distributed independently from the host system they are used on, and they are isolated from the host system ('sandboxed') to some degree, at runtime.

Install apps:

```bash

```

## [Multimedia codecs](https://docs.fedoraproject.org/en-US/quick-docs/installing-plugins-for-playing-movies-and-music/)

> As a Fedora user and system administrator, you can use these steps to install additional multimedia plugins that enable you to play various video and audio types. 

```shell
sudo dnf update @multimedia --setopt="install_weak_deps=False" --exclude=PackageKit-gstreamer-plugin
```

> Fedora ffmpeg-free works most of the time, but one will experience version missmatch from time to time. Switch to the rpmfusion provided ffmpeg build that is better supported. You will still need to follow the next section for additional codecs or plugins related to packages you might have installed. 

```shell
sudo dnf swap ffmpeg-free ffmpeg --allowerasing
```


## Drivers

<img src="https://upload.wikimedia.org/wikipedia/sco/2/21/Nvidia_logo.svg" width="17%" align="right" />

**nVidia**

> ⚠️ **NOTE:** Install [RPM Fusion](#rpm-fusion) first.

```bash
sudo dnf install akmod-nvidia
```
