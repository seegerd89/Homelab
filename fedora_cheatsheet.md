<img src="https://cdn.svgporn.com/logos/fedora.svg" width="30%" align="right" />

<h1>Fedora CheatSheet</h1>

- [Packages](#packages)
  - [RPM Fusion](#rpm-fusion)
  - [DNF](#dnf)
    - [DNF Config](#dnf-config)
    - [DNF Packages](#dnf-packages)
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

#### DNF Config
```bash
CONFIG_FILE="/etc/dnf/dnf.conf" && PARAMS=(
  "defaultyes=True" # Select Y by default.
) && for PARAM in ${PARAMS[@]}; do
  grep "^$PARAM" $CONFIG_FILE || echo $PARAM | sudo tee -a $CONFIG_FILE
done
```

#### DNF Packages

```bash
APPS=(
  https://downloads.1password.com/linux/rpm/stable/x86_64/1password-latest.rpm
  https://dl.google.com/linux/direct/google-chrome-stable_current_x86_64.rpm
  https://zoom.us/client/latest/zoom_x86_64.rpm
  https://download.teamviewer.com/download/linux/teamviewer.x86_64.rpm
  
  @development-tools # Build-essentials analog.
  conda              # Python-agnostic package manager
  python3-virtualenv # Tool to create isolated Python environments
  zeal               # Offline documentation viewer

  exfat-utils         # Utilities to create, check, label and dump exFAT file system 
  htop                # Terminal system monitor
  java-latest-openjdk # Jave development kit
  jq                  # Takes JSON input and retrieves data by query
  mc                  # Two panel terminal file manager
  neofetch            # Shows Linux System Information with Distribution Logo
  net-tools           # Base network tools
  stacer              # Cool CleanMyMac alternative
  timeshift           # Backup utility

  arj   # arj archiver
  lha   # lzh unarchiver
  unrar # rar unarchiver

  libreoffice
  libreoffice-langpack-{uk,ru}
  libreoffice-help-{uk,ru}

  libheif-{freeworld,tools} # Tools for reading and manipulating HEIF files

  clementine       # Audio/Radio/Podcasts player
  dia              # Diagram editor
  evolution        # Outlook alternative
  evolution-ews    # Evolution Exchange support
  ffmpeg           # Universal media transcoder tool
  flameshot        # Powerful and simple to use screenshot software
  foliate          # Simple and modern GTK eBook reader
  inkscape         # Vector image editor
  kiwix-desktop    # Offline Wikipedia downloader/viewer
  telegram-desktop # Best IM!
  transmission     # Torrent client
  vlc
) && sudo dnf install -y ${APPS[*]} 
```

<img src="https://upload.wikimedia.org/wikipedia/commons/1/1a/Flatpak_logo.png" width="17%" align="right" />

### Flatpak

> Flatpak is a tool for managing applications and the runtimes they use. In the Flatpak model, applications can be built and distributed independently from the host system they are used on, and they are isolated from the host system ('sandboxed') to some degree, at runtime.

Add [flathub](https://flathub.org) remote:

```bash
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
```

Install apps:

```bash
curl https://raw.githubusercontent.com/alexander-danilenko/fedora-environment/main/config.yml | yq -rc '.apps.flatpak[]' | xargs flatpak install -y flathub
```

> ⚠️ **NOTE:** `yq` [python package](#python) is required

Fix cursors:

```bash
flatpak --user override --filesystem=/home/$USER/.icons/:ro 
flatpak --user override --filesystem=/home/$USER/.local/share/:ro
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

## Terminal

<img src="https://upload.wikimedia.org/wikipedia/commons/1/1f/Z_Shell_Logo_Color_Horizontal.svg" width="17%" align="right" />

### [Fish Shell](https://fishshell.com/)

<img src="https://fishshell.com/assets/img/Terminal_Logo_LCD_Small.png" width="17%" align="right" />

> Fish is a smart and user-friendly command line
shell for Linux, macOS, and the rest of the family.

Install `fish`:

```bash
sudo apt install -y fish
```

Set it as default for current user:

```bash
chsh -s $(which fish) && sudo !!
```

Copy configs:

```bash
mkdir -p $HOME/.config/fish/ && \
curl -L# -o $HOME/.config/fish/config.fish https://raw.githubusercontent.com/alexander-danilenko/dotfiles/main/.config/fish/config.fish && \
curl -L# -o $HOME/.config/fish/fish_variables https://raw.githubusercontent.com/alexander-danilenko/dotfiles/main/.config/fish/fish_variables
```

**[Oh My Fish](https://github.com/oh-my-fish/oh-my-fish)**: Package manager

> [Oh My Fish](https://github.com/oh-my-fish/oh-my-fish) provides core infrastructure to allow you to install packages which extend or modify the look of your shell. It's fast, extensible and easy to use..

Install `oh-my-fish`:

```bash
curl https://raw.githubusercontent.com/oh-my-fish/oh-my-fish/master/bin/install | fish
```

Run `fish` and install plugins:

```bash
omf install (curl https://raw.githubusercontent.com/alexander-danilenko/fedora-environment/main/config.yml | yq -rc '.fish.packages[]')
```

### Extend inotify

> https://youtrack.jetbrains.com/articles/IDEA-A-2/Inotify-Watches-Limit
>
> Inotify requires a "watch handle" to be set for each directory in the project. Unfortunately, the default limit of watch handles may not be enough for reasonably sized projects, and reaching the limit will force IntelliJ platform to fall back to recursive scans of directory trees.
>
> To prevent this situation it is recommended to increase the watches limit (to, say, 512K)

```bash
grep '^fs.inotify.max_user_watches=524288' /etc/sysctl.conf || \
echo  'fs.inotify.max_user_watches=524288' | sudo tee -a /etc/sysctl.conf && sudo sysctl -p
```

## Development

<img src="https://cdn.svgporn.com/logos/python.svg" width="17%" align="right" />

### Python

> Python is an interpreted, interactive, object-oriented programming language that combines remarkable power with very clear syntax.

Install Python and its package manager

```bash
sudo dnf install python3 python3-pip python3-virtualenv pipenv
```

Install `yq` for parsing yml files format.

```bash
pip install yq
```

Install packages:

```bash
curl https://raw.githubusercontent.com/alexander-danilenko/fedora-environment/main/config.yml | yq -rc '.python3.pip3_global_packages[]' | xargs pip install
```

<img src="https://cdn.svgporn.com/logos/nodejs.svg" width="17%" align="right" />

### Node.JS

> [`NVM`](https://github.com/nvm-sh/nvm) allows you to quickly install and use different versions of node via the command line.

Install NVM:

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.0/install.sh | bash
```

Install LTS and set as default:

```bash
nvm install --lts && nvm alias default "lts/*"
```

Install global packages:

```bash
curl https://raw.githubusercontent.com/alexander-danilenko/fedora-environment/main/config.yml | yq '.node.npm_global_packages[]' -cr | xargs npm install --global
```
> ⚠️ **NOTE:** `yq` [python package](#python) is required

<img src="https://cdn.svgporn.com/logos/php.svg" width="17%" align="right" />

### PHP

```bash
sudo dnf install -y php-{common,cli,curl,gd,json,mbstring,mysqli,opcache,pdo,xml,zip}
```

Composer

```bash
mkdir -p $HOME/.composer && \
sudo curl -#fsSL https://getcomposer.org/composer-stable.phar -o /usr/local/bin/composer && \
sudo chmod 755 /usr/local/bin/composer && \
composer --version && \
composer global require drupal/coder squizlabs/php_codesniffer friendsofphp/php-cs-fixer && \
cp -rf \
  ~/.composer/vendor/drupal/coder/coder_sniffer/Drupal* \
  ~/.composer/vendor/squizlabs/php_codesniffer/src/Standards
```

<img src="https://cdn.svgporn.com/logos/jetbrains.svg" width="17%" align="right" />

### JetBrains Toolbox
```bash
curl -Ls https://raw.githubusercontent.com/nagygergo/jetbrains-toolbox-install/master/jetbrains-toolbox.sh | bash
```

<img src="https://cdn.svgporn.com/logos/visual-studio-code.svg" width="17%" align="right" />

### Visual Studio Code

Add rpm repo and install `code` package

```bash
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo' && \
sudo dnf check-update && sudo dnf install -y code && \
curl -L# -o $HOME/.config/Code/User/settings.json --create-dirs https://raw.githubusercontent.com/alexander-danilenko/dotfiles/main/.config/Code/User/settings.json
```

Install extensions

```bash
curl https://raw.githubusercontent.com/alexander-danilenko/fedora-environment/main/config.yml | yq .apps.visual_studio_code.extensions[] -cr | while read extension; do
    code --install-extension $extension --force
done
```
> ⚠️ **NOTE:** `yq` [python package](#python) is required

<img src="https://cdn.svgporn.com/logos/sublimetext-icon.svg" width="17%" align="right" />

### Sublime Apps

```bash
sudo rpm -v --import https://download.sublimetext.com/sublimehq-rpm-pub.gpg && \
sudo dnf config-manager --add-repo https://download.sublimetext.com/rpm/stable/x86_64/sublime-text.repo && \
sudo dnf install -y sublime-text sublime-merge && \
curl -L# -o $HOME/.config/sublime-text-3/Packages/User/Preferences.sublime-settings --create-dirs https://raw.githubusercontent.com/alexander-danilenko/dotfiles/main/.config/sublime-text-3/Packages/User/Preferences.sublime-settings
```

<img src="https://upload.wikimedia.org/wikipedia/commons/9/98/Logo_of_WireGuard.svg" width="17%" align="right" />

## Wireguard VPN

### Server

Quick setup script: https://github.com/Nyr/wireguard-install

```bash
wget https://git.io/wireguard -O wireguard-install.sh && bash wireguard-install.sh
```

### Client (Fedora)

- Install prerequisites:
  ```bash
  sudo dnf install wireguard-tools
  ```
- Copy config to `/etc/wireguard/wg0.conf` file
- ! Make sure port from config is whitelisted in firewall: `sudo ufw allow 58320/udp`
- Enable autostart: `sudo systemctl enable wg-quick@wg0`
- Disable autostart: `sudo systemctl disable wg-quick@wg0`
- Start: `sudo systemctl start wg-quick@wg0`
- Stop: `sudo systemctl stop wg-quick@wg0`
- Status: `sudo systemctl status wg-quick@wg0`

```python
#!/usr/bin/env python3

import click
import subprocess

@click.command(help='Manages Wireguard VPN.')
@click.argument('action', type=click.Choice(['start', 'stop', 'enable', 'disable', 'status']))
@click.option('--config', help='Config name.', default='wg0')
def wireguard_manager(action, config):
    if action in ['start', 'stop', 'enable', 'disable', 'status']:
        subprocess.call(f'set -ex && sudo systemctl {action} wg-quick@{config}', shell=True)

if __name__ == '__main__':
    wireguard_manager()
```

## Containerization

<img src="https://cdn.svgporn.com/logos/docker.svg" width="17%" align="right" />

### Docker

Make sure current release version added in: https://download.docker.com/linux/fedora/

```bash
sudo dnf remove -y docker-{client,client-latest,common,latest,latest-logrotate,logrotate,selinux,engine-selinux,engine} && \
sudo dnf config-manager --add-repo https://download.docker.com/linux/fedora/docker-ce.repo && \
sudo dnf install -y docker-ce docker-compose && \
sudo usermod -aG docker $USER && \
sudo systemctl enable docker && \
sudo systemctl restart docker && \
newgrp docker
```

### Docksal

```bash
bash <(curl -fsSL https://get.docksal.io)
```

## Desktop

### GTK Themes / Icons

```bash
APPS=(
  papirus-icon-theme
  materia-gtk-theme
  paper-icon-theme
  yaru-theme
  yaru-sound-theme
  yaru-icon-theme
  yaru-gtk3-theme
  yaru-sound-theme
  breeze-cursor-theme
) && sudo dnf install -y ${APPS[*]}
```

<!-- 
### Microsoft Fonts

> When it comes to typography, Microsoft True Type fonts have entirely dominated the market. Although we have more than a thousand fonts available, the extensive use of the Windows operating system has altogether led to the increase in popularity of Microsoft True Type fonts. 
> 
> Some of them like the “Times New Roman (Bold, Italic, Bold Italic)” are recommended in most documents and many writing formats like APA, MLA, Harvard, etc. and regarded as standard fonts. Microsoft True Type fonts are also in most webpages, and you can find this declared in the style sheets.

Install Microsoft Fonts to the system:

```bash
sudo rpm -i https://downloads.sourceforge.net/project/mscorefonts2/rpms/msttcore-fonts-installer-2.6-1.noarch.rpm
```
-->

### Google Fonts

List fonts available to install: 

```bash
curl https://gwfh.mranftl.com/api/fonts | jq '.[].id' -cr | sort
```

Install needed fonts:

```bash
FONTS_DIR="$HOME/.fonts"
FONTS=(
  jetbrains-mono
  open-sans
  roboto
  roboto-mono
  roboto-slab
  ubuntu
  ubuntu-mono
) && \
mkdir -p $FONTS_DIR && \ 
for FONT in ${FONTS[@]}; do
  DOWNLOAD_URL="https://gwfh.mranftl.com/api/fonts/${FONT}?download=zip&formats=ttf"
  FILE_PATH="/tmp/$FONT-ttf.zip"
  curl "$DOWNLOAD_URL" -o "$FILE_PATH"
  unzip -o $FILE_PATH -d $FONTS_DIR
done
```

Update fonts cache (may take a while): `sudo fc-cache -f -v`

### Gnome

Gnome Tweaks:
```bash
sudo dnf install -y gnome-tweaks gnome-extensions-app
```

#### Gnome Extensions

| Name        | Description |
|------------:|:------------|
| [Battery Percentage (for laptops)](https://extensions.gnome.org/extension/818) | Show battery remaining power percentage at the top panel |
| [Blyr](https://extensions.gnome.org/extension/1251) | Blur Effect to GNOME Shell UI elements |
| [Compiz alike magic lamp effect](https://extensions.gnome.org/extension/3740) | Magic lamp effect for minimizing windows |
| [Compiz windows effect](https://extensions.gnome.org/extension/3210) | Compiz wobbly windows effect |
| [Dash to Dock](https://extensions.gnome.org/extension/307) | This extension moves the dash out of the overview transforming it in a dock for an easier launching of applications and a faster switching between windows and desktops |
| [Dash to Panel](https://extensions.gnome.org/extension/1160) | Moves the dash into the gnome main panel so that the application launchers and system tray are combined into a single panel, similar to that found in KDE Plasma and Windows 7+ |
| [Emoji Selector](https://extensions.gnome.org/extension/1162) | Provides a parametrable popup menu displaying most emojis, clicking on an emoji copies it to the clipboard |
| [Hide Activities Button](https://extensions.gnome.org/extension/744) | Hides the Activities button from the status bar |
| [Notification Alert](https://extensions.gnome.org/extension/258) | Whenever there is an unread notification (e.g. chat messages), blinks the message in the user's menu with a color chosen by the user |
| [Sound Input & Output Device Chooser](https://extensions.gnome.org/extension/906) | Shows a list of sound output and input devices (similar to gnome sound settings) in the status menu below the volume slider |
| [Tray Icons: Reloaded](https://extensions.gnome.org/extension/2890) | Bring back Tray Icons to top panel, with additional features |
| [User Themes](https://extensions.gnome.org/extension/19) | Gnome Shell themes support |
| [Wireless HID](https://extensions.gnome.org/extension/4228) | Shows the battery of the wireless keyboards, mice, and game controllers in percentages and colors |

## Tweaks

### Alsamixer save configuration

Save `alsamixer` settings once set: this should save alsamixer configurations to `/etc/asound.state` which gets loaded every startup.

```shell
sudo alsactl store
```

### User Dirs in Synology Drive

`~/.config/user-dirs.dirs`

```bash
XDG_DESKTOP_DIR="$HOME/SynologyDrive/Desktop"
XDG_DOWNLOAD_DIR="$HOME/Downloads"
XDG_TEMPLATES_DIR="$HOME/SynologyDrive/Templates"
XDG_PUBLICSHARE_DIR="$HOME/SynologyDrive/Public"
XDG_DOCUMENTS_DIR="$HOME/SynologyDrive/Documents"
XDG_MUSIC_DIR="$HOME/SynologyDrive/Media/Music"
XDG_PICTURES_DIR="$HOME/SynologyDrive/Media/Pictures"
XDG_VIDEOS_DIR="$HOME/SynologyDrive/Media/Videos"
```

### NFS Shares

Create directories first: 

```bash
sudo mkdir -p /mnt/NAS/{Homes,Media}
```

Add to `/etc/fstab`:
```
192.168.50.123:/volume1/homes     /mnt/NAS/Homes      nfs defaults 0 0
192.168.50.123:/volume1/Media     /mnt/NAS/Media      nfs defaults 0 0
```

### SWAP

Set swap to x2 of current ram:

`/etc/systemd/zram-generator.conf`:
```bash
[zram0]
max-zram-size = none
zram-fraction = 2
```

### Boot into last booted grub record

In `/etc/default/grub` 

Set:
```
GRUB_DEFAULT=saved
GRUB_SAVEDEFAULT=true
```

Then apply the grub updates to grub config:
```bash
sudo grub2-mkconfig -o /boot/grub2/grub.cfg
```

### Fix Flatpak Postman crash 

```
cd ~/.var/app/com.getpostman.Postman/config/Postman/proxy && openssl req -subj '/C=US/CN=Postman Proxy' -new -newkey rsa:2048 -sha256 -days 365 -nodes -x509 -keyout postman-proxy-ca.key -out postman-proxy-ca.crt && cd -
```
