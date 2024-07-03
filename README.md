<h1 align="center">
<a href='#'><img src="https://raw.githubusercontent.com/catppuccin/catppuccin/main/assets/palette/macchiato.png" width="600px"/></a>
  <br>
  <div>
    </a>
    <a href="https://github.com/redyf/nixdots/LICENSE">
        <img src="https://img.shields.io/static/v1.svg?style=for-the-badge&label=License&message=MIT&logoColor=ca9ee6&colorA=313244&colorB=cba6f7"/>
    </a>
    <br>
    </div>
        <img href="https://builtwithnix.org" src="https://builtwithnix.org/badge.svg"/>
   </h1>

<div align="center">
<h1>
❄️ NixOS dotfiles ❄️
</h1>
</div>
<h2 align="center">NixOS system configu.</h2>

```mint
⠀⠀   🌸 Setup / Hyprland 🌸
 -----------------------------------
 ╭─ Distro  -> NixOS
 ├─ Editor  -> Neovim
 ├─ Browser -> Firefox
 ├─ Shell   -> ZSH
 ╰─ Resource Monitor -> Btop
 ╭─ MB -> HP Omen MB
 ├─ CPU   -> Ryzen 5800x
 ├─ GPU   -> NVIDIA RTX-3060TI & RTX 4080 
 ╰─ Resolution -> 1920x1080@165hz
 ╭─ WM       -> Hyprland
 ├─ Terminal -> Wezterm
 ├─ Theme    -> Catppuccin
 ├─ Icons    -> Papirus-Dark
 ├─ Font     -> JetBrains Mono Nerd Font
 ╰─ Hotel    -> Trivago
                        
```

<hr>

<div align="center">

![rice showcase](./assets/showcase.png)
![rice showcase2](./assets/showcaseoxocarbon.png)

</div>

<hr>

## Commands you should know:

- Rebuild and switch to change the system configuration (in the configuration directory):

```
nh os switch
```

OR

```
sudo nixos-rebuild switch --flake '.#redyf'
```

- Connect to internet (Change what's inside the brackets with your info).

```
iwctl --passphrase [passphrase] station [device] connect [SSID]
```

## Installation

<strong>

Only follow these steps after using the bootable drive.

</strong>

```
First part:
video=1920x1080
setfont ter-128n
configure networking as needed (skip this if you're using ethernet)
sudo -i
lsblk (check info about partitions and the device you want to use for the installation)
gdisk /dev/vda (change according to your system, for me it's /dev/nvme0n1)
then configure 600M type ef00, rest ext4 type 8300 as described below
Type "n" to make a new partition, choose the partition number, first sector can be default but last sector should be 600M. Hex code for EFI is ef00.
Now type n again to make another partition, this time we'll leave everything as default. After finishing these steps, make sure to write it to the disk by typing "w".
lsblk
mkfs.fat -F 32 -n boot /dev/vda1 (Format the partitions)
mkfs.ext4 -L nixos /dev/vda2
mount /dev/disk/by-label/nixos /mnt (Mount partitions)
mkdir /mnt/boot (Create a directory for boot)
mount /dev/disk/by-label/boot /mnt/boot
```

After mounting the partitions, you can move to the second part...

```
# go inside a nix shell with the specified programs
nix-shell -p git nixUnstable neovim
# create this folder if necessary
mkdir -p /mnt/etc/
# clone the repo
git clone https://github.com/redyf/nixdots.git /mnt/etc/nixos --recurse-submodules
# remove this file
rm /mnt/etc/nixos/hosts/redyf/hardware-configuration.nix
# generate the config and take some files
nixos-generate-config --root /mnt
rm /mnt/etc/nixos/configuration.nix
mv /mnt/etc/nixos/hardware-configuration.nix /mnt/etc/nixos/hosts/redyf/
# make sure you're in this path
cd /mnt/etc/nixos
# Install my config:
nixos-install --flake '.#redyf'
# Obs:
If you'd like to use my config as a template, all you need to do is replace "redyf" with your username.
```

</details>
<hr>

</details>



## Conclusion

That should be all!

The code is licensed under the MIT license, so you can use or distribute the code however you like.
