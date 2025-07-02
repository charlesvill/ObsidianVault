- how to naviagte to different workspaces
	- super+ctrl+arrowup/down

website for the different keybindings: https://support.system76.com/articles/pop-keyboard-shortcuts/




good website for customizing gnome desktop environment: https://khushwant.hashnode.dev/ricing-tweaking-gnome-look-and-feel

sick color scheme and config files for neovim: https://github.com/xero/dotfiles

video on good gnome extensions: https://www.youtube.com/watch?v=AE1-W2bMVEs

installing linux the right way: https://www.youtube.com/watch?v=10f4899srvc

beautiful warm ghibli looking wallpaper: https://www.reddit.com/r/wallpaper/comments/15bcdij/train_crossing_the_sea_1920_x_1080/

warm color theme for gnome: https://www.gnome-look.org/p/1283955/

cozy rice inspo using the graphite gtk theme: https://www.reddit.com/r/unixporn/comments/t73gvt/gnome_cozy_first_rice/

literal fnv rice: https://www.reddit.com/r/unixporn/comments/i18k0e/qtile_fallout_new_vegas_rice/


so far the ideal set up: 
1. zsh & oh my zsh
2. pop-shell for tiling manager: see guide https://github.com/pop-os/shell
3. neovim with sick config files
4. btop for resource monitoring
5. cava for audio visualizer
6. gruvbox gtk theme: https://www.gnome-look.org/p/1681313/
7. foliate for the book reader
8. time shift to create back ups
9. power management: https://www.youtube.com/watch?v=kTFnGwW2e_Y
10. auto cpu-freq
11. flameshot for screenshotting
12. program to monitor intel graphics usage: intel-gpu-tools found in apt repo
	1. command to run is `sudo intel_gpu_top`
13. go to this github to install proton GE custom: https://github.com/GloriousEggroll/proton-ge-custom#installation
	1. install first vulkan drivers for intel: https://github.com/lutris/docs/blob/master/InstallingDrivers.md
	2. see this video on getting mods and such to run on fallout new vegas:  https://www.youtube.com/watch?v=AqpQC1htuic&t=35s&ab_channel=Bleeplo
	3. see this guide on optimizing the performance of fallout new vegas: 
		1. start here: https://vivanewvegas.moddinglinked.com/ then...
		2. https://performance.moddinglinked.com/falloutnv.html
		3. directory path: Instance type: Global

Instance location: C:\users\steamuser\AppData\Local\ModOrganizer\New Vegas - debian12
Instance name: New Vegas - debian12
Game location: Z:\home\general-iroh\.local\share\Steam\steamapps\common\Fallout New Vegas


14. make sure for development environment you have the following: 
	1. apt install git
	2. ssh key set up
	3. visual studio code
	4. node package manager
	5. obsidian & obsidin git

grub> command line commands

```
set prefix=(hd0,gpt1)/grub

insmod linux
set root=(hd0,gpt3)
linux (hd0,gpt1)/vmlinuz-linux root=/dev/sda3
initrd (hd0,gpt1)/initramfs-linux.img
boot

```

### arch linux rebuilding uefi boot configuration, kernel and efi file structure
## ✅ Final Pre-boot Checklist

1. **Kernel + initramfs** are in `/boot`:
    
    bash
    
    CopyEdit
    
    `ls /boot/vmlinuz-linux /boot/initramfs-linux.img`
    
2. **Intel microcode** is present and referenced in GRUB:
    
    bash
    
    CopyEdit
    
    `grep intel-ucode /boot/grub/grub.cfg`
    
3. **EFI partition (`/dev/sda1`) is mounted at `/efi`**, not `/boot`:
    
    bash
    
    CopyEdit
    
    `mount | grep efi`
    
4. **GRUB EFI binary was installed to the ESP**:
    
    bash
    
    CopyEdit
    
    `grub-install --target=x86_64-efi --efi-directory=/efi --bootloader-id=GRUB`
    
5. **GRUB config was generated** and includes Arch:
    
    bash
    
    CopyEdit
    
    `grep menuentry /boot/grub/grub.cfg`
    
    Output should include:
    
    nginx
    
    CopyEdit
    
    `menuentry 'Arch Linux'`
    
6. Optional but recommended: **Check that efibootmgr lists GRUB**
    
    bash
    
    CopyEdit
    
    `efibootmgr`
    
    You should see something like:
    
    CopyEdit
    
    `Boot0001* GRUB`
    

---

## ✅ Now you can:

bash

CopyEdit

`exit umount -R /mnt reboot`

---

## 🖥️ On Reboot:

- Make sure your BIOS/UEFI is set to **boot from the correct drive** (the one where the ESP is `/dev/sda1`)
    
- You should now see the **GRUB menu** with an **"Arch Linux"** entry
    
- If it boots and lands you at a login prompt or desktop (if installed), you’re golden
    

---

If it doesn’t boot or drops to GRUB rescue/shell again, don’t worry — just tell me what you see, and I’ll help you get back in and fix it fast.

But based on everything you've done, **you’re 99% good to go** 🚀

##### You said:

give me this list you just gave me as markdown text

###### ChatGPT said:

Sure! Here's the checklist in **Markdown** format:

markdown

CopyEdit

``# ✅ Final Pre-Boot Checklist for Arch Linux (UEFI with GRUB)  ## 1. Kernel + initramfs are in `/boot` ```bash ls /boot/vmlinuz-linux /boot/initramfs-linux.img``

## 2. Intel microcode is present and referenced in GRUB

bash

CopyEdit

`grep intel-ucode /boot/grub/grub.cfg`

## 3. EFI partition (`/dev/sda1`) is mounted at `/efi` (not `/boot`)

bash

CopyEdit

`mount | grep efi`

## 4. GRUB EFI binary is installed to the ESP

bash

CopyEdit

`grub-install --target=x86_64-efi --efi-directory=/efi --bootloader-id=GRUB`

## 5. GRUB config was generated and includes Arch

bash

CopyEdit

`grep menuentry /boot/grub/grub.cfg`

Expected output:

nginx

CopyEdit

`menuentry 'Arch Linux'`

## 6. (Optional) GRUB is listed in UEFI boot entries

bash

CopyEdit

`efibootmgr`

Expected output:

CopyEdit

`Boot0001* GRUB`

---

# ✅ Ready to Reboot

bash

CopyEdit

`exit umount -R /mnt reboot`

Make sure your BIOS/UEFI is set to boot from the correct drive (`/dev/sda`).

On reboot, you should see the GRUB menu with an "Arch Linux" entry.

### file structure: 
```
/boot/
├── vmlinuz-linux            # The Linux kernel binary
├── initramfs-linux.img      # Initial RAM filesystem image
├── initramfs-linux-fallback.img  # Backup initramfs image
├── intel-ucode.img          # Intel CPU microcode update image
├── grub/                    # GRUB configuration and modules
│   ├── fonts/
│   ├── i386-pc/
│   ├── locale/
│   ├── themes/
│   └── grub.cfg             # Main GRUB config file generated by grub-mkconfig
└── System.map-linux          # Kernel symbol table (optional)

```

```
/efi/
├── EFI/
│   ├── GRUB/
│   │   └── grubx64.efi        # GRUB UEFI bootloader binary
│   ├── Boot/
│   │   └── bootx64.efi        # Default/fallback UEFI bootloader
│   ├── Microsoft/             # Windows boot files (if dual boot)
│   └── <other OS folders>/    # Other OS bootloaders, if present
├── PK                        # Platform Key (if Secure Boot enabled)
├── KEK                       # Key Exchange Key (Secure Boot)
├── db                        # Allowed signatures (Secure Boot)
├── dbx                       # Revoked signatures (Secure Boot)
└── (possibly other EFI apps)

```