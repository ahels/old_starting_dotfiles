# dotfiles
Linux dotfiles


# Endeavour OS SWAY set up

To quit sway:
> Super + Shift + e

To start sway:
> sway

To reload sway:
> Super + Shift + c

## Basic packages
Install sway and important related packages:
- sway
- swayidle
- swaylock

### Other important stuff
- **Shell**: zsh
- **Terminal**: kitty
- **Editor**:neovim

From AUR (with yay [Do not use sudo!!])
- **Launcher**: rofi-lbonn-wayland

## Set up basic configuration
- Create the sway config directory  *.config/sway*.
- Copy the default config file (or copy your own config file) from */etc/sway/config* to *~/.config/sway*. 
- Edit de defaults:
	* Set new variable for Alt key (set $altkey Mod1)
	* Set terminal by the one you selected (kitty).
	* Change your launcher (rofi -show drun)
	* Change default shortcut to open the menu ($altkey+space)
Then you can start sway and configure it.

### Install autotiling
Install it via yay(AUR) with the name *autotiling*.
Add the exec command to run the script on sway start for the desired workspac
> exec autotiling -w

## Change the shell 
Be sure the shell is installed:
> zsh --version

List the available shells (paths):
> chsh -l

Change the shell:
> chsh -s *path*

Reboot the system

Set it up

## Theming the shell

### Oh my zsh
Go to their github and install via curl, wget or fetch (check which do you have on your system). Copy the command and run it on the terminal to copy the repository.

### Installing a nerd font
Nerd fonts are very useful, because they have icons included in their own. 
> JetBrains Mono is one of them and is well suited for programming. 

- Go to official page and download the desired one.
- Create a new directory to host fonts
	* ~/.local/share/fonts
	* It can be useful to add another directory for better fonts administration. For example, store it on a new directory nerd_fonts or ttf.
- Move the font zip to the new directory
- Unzip and remove the zip file
- Reload system fonts
> fc-cache -vf
- Restart system
- Aliases the new installed font
> fc-match *font_name* -a

### Change the terminal font

**Kitty**
Open kitty and pulse *ctrl+shift+F2* to create/open the config file.
Uncomment and change default font with the new you have installed and renamed. The point font size of the terminal can be setted to, for example 22.

Open a new kitty terminal to verify the font and the size are well configured

### powerlevel10k
Go to its github and follow the installation guide. Manual is the recommended one.
Reopen the terminal to run auto configuration aid. It can be launched with *p10k* command.

Follow the steps to configure it

## Display manager
There are not a lot of options
- gdm (too many dependencies)
- ly (tty based)
- greetd (in early stage, and lack of examples)

### ly
It has problems with multiple different dpi displays 
- Install de package
- Enable the service
> sudo systemctl enable ly.service

### Display Manager: greetd + gtkgreet
Install the packages from AUR via yay.
- install **Display Manager**: greetd
- install a **greeter** (gtkgreet): greetd-gtkgreet
Enable the service
> sudo systemctl enable greatd.service

Specify the available login environments on */etc/greetd/environments* file. In this case only sway is required:
> sway

Create a configuration file */etc/greetd/sway-config* to be used with sway as compositor for gtkgreet. To change the default theme, specify it on exec line adding *"GTK_THEME=Name_theme"*. For example: *exec "GTK_THEME=Adwaita-dark gtkgreat -l;swaymsg exit"*
> # `-l` activates layer-shell mode. Notice that `swaymsg exit` will run after gtkgreet.
> exec "gtkgreet -l; swaymsg exit"
>
> bindsym Mod4+shift+e exec swaynag \
> -t warning \
> -m 'What do you want to do?' \
> -b 'Poweroff' 'systemctl poweroff' \
> -b 'Reboot' 'systemctl reboot'
>
> include /etc/sway/config.d/*

Set sway as to start greetd on */etc/greetd/config.toml *  file (change command line):
> command = "sway --config /etc/greetd/sway-config"

**NOTE**: It is possible to add more theming options (like mouse pointer, icons...). For example, adding this options before exec "gtkgreet":
> exec {
>	gsettings set org.gnome.desktop.interface gtk-theme 'Yaru'
>	gsettings set org.gnome.desktop.interface icon-theme 'Yaru'
>	gsettings set org.gnome.desktop.interface cursor-theme 'Yaru'
> }


## Sway customization/config
###Wallpaper
Install swaybg and change the output on config file
> output "*" bg /path/to/image fill

### System theming
Search for theme available themes to be used. For example, * gnome-themes-extra* allows to use Adwaita themes (light and dark) 

To configure it via GUI, install *lxappearance*. (Needs xwayland to run)

### Cursors
- Capitaine theme is cool and is avialable on official Arch repositories

-----------
*swayidle -> allow to suspend on inactivity 

- xwayland
- font
- oh-my-zsh
- powerlevel10k
- display manager
--- **X App support**: xwayland

### Important packages than can be installed through calamares
-**Backlight control**: light 
-**Audio**: pulseaudio pulseaudio-alsa alsa-utils
-**Bluetooth**: bluez

### Other software
**PDF editing** xournalpp
**File Manager** thunar/ranger
**Theming and customization** lxappearance
**XWayland (Use of X based apps)** xorg-wayland
**Audio** pipeware
