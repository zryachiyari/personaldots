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
sudo nixos-rebuild switch --flake '.#ari'
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

sudo -i

lsblk -f (find info about partitions and the device you want to use for the installation)

gdisk /dev/[drive] (change according to your system, for me it's /dev/nvme0n1)

#time to config drives 

Type "n" to make a new partition, choose the partition number, leave first sector alone, but last sector should be 600M. enter the hex code for EFI it is ef00.

Now type n again to make another partition, this time we'll leave everything as default. So spam enter. After finishing these steps, make sure to write it to the disk by typing "w".

lsblk -f again, make sure everything is correctly wrote, you should see two pations numbered accordingly.

# Now we format the partitions we just made.

mkfs.fat -F 32 -n BOOT /dev/[your drive, partition one.]

mkfs.ext4 -L NIXOS /dev/[your drive, partition two.]

# Now we mount these bad boys.

mount /dev/disk/by-label/NIXOS /mnt
mkdir /mnt/boot 
mount /dev/disk/by-label/BOOT /mnt/boot
```

After creating and mounting the partitions, you can move to the second part... great job so far!!! <3

```
# Enter a nix shell with the specified programs, you should use neovim to edit my dots to personalize stuff.

nix-shell -p git nixUnstable neovim

# Create this folder if necessary

mkdir -p /mnt/etc/

# clone my repo

git clone https://github.com/zryachiy/personaldots.git /mnt/etc/nixos --recurse-submodules

# remove my hardware config file

rm /mnt/etc/nixos/hosts/ari/hardware-configuration.nix

# generate a new hardware config just for you!

nixos-generate-config --root /mnt
rm /mnt/etc/nixos/configuration.nix
mv /mnt/etc/nixos/hardware-configuration.nix /mnt/etc/nixos/hosts/ari/

# now move to this path
cd /mnt/etc/nixos

# now just unstall my config!:
nixos-install --flake '.#ari'


remember! if you'd like to use my config as a template, all you need to do is replace "ari" with your username!
```

</details>
<hr>

</details>



## Conclusion

That should be all!
Thank you to user "redyf" as this is heavily inspired by their template.
The code is licensed under the MIT license, so you can use or distribute the code however you like.
