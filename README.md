# ASUS Zenbook UX3405MA amplifier
SSDT Patch to fix missing speakers sound on Asus Zenbook 14 UX3405MA (2024) and latest BIOS

> [!NOTE]
> Deprecated! ≥ 6.11 Linux Kernel
>
> Added support for **10431A63**
>
> https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux.git/tree/sound/pci/hda/cs35l41_hda_property.c?h=v6.11

**BIOS Configuration**

- **BIOS Version:** Tested on 305
- **Secure Boot:** Disabled
- **Tested OS:** Fedora 39 kernel-6.8.6-200.fc39.x86_64

# Patch installation

## Arch based
Install AUR package, created by [tholden92](https://github.com/tholden92):

[![AUR](https://img.shields.io/aur/version/zenbook-sound-fix-ux3405ma)](https://aur.archlinux.org/packages/zenbook-sound-fix-ux3405ma/)

## Package/repo installation (via OBS)
See instructions to install compiled aml as binary package for ArchLinux, Fedora, Debian, openSUSE, Ubuntu here:

[![build result](https://build.opensuse.org/projects/home:smallcms/packages/zenbook-sound-fix-ux3405ma/badge.svg?type=percent)](https://software.opensuse.org//download.html?project=home%3Asmallcms&package=zenbook-sound-fix-ux3405ma)

## Manual installation

### Build the _ssdt-csc3551.dsl_

```
iasl -tc ssdt-csc3551.dsl
```

### Copy it to /boot

```
sudo cp -f ssdt-csc3551.aml /boot
```

### Copy grub script

```
sudo cp -f 01_acpi /etc/grub.d && sudo chmod +x /etc/grub.d/01_acpi
```

### Update grub config

* Update grub config
  * Debian / Ubuntu based distributions

    ```sudo update-grub```

  * Fedora / RHEL-based distributions

    ```sudo grub2-mkconfig -o /etc/grub2.cfg```

    ```sudo grub2-mkconfig -o /etc/grub2-efi.cfg```

  * Arch based distributions

    ```grub-mkconfig -o /boot/grub/grub.cfg```

### Reboot

# Bonus: Fix pop/crack when stop playback, audio cutting out

Copy pipewire and wireplumber config parts to user's home ~/.config

```
cp -r fix_pop_crack_pop/pipewire ~/.config
```
> [!NOTE]
> If you are using wireplumber before 0.5, copy this lua
```
cp -r fix_pop_crack_pop/wireplumber/main.lua.d ~/.config/wireplumber
```
> [!NOTE]
> If you have modern wireplumber 0.5 or higher, copy this conf
```
cp -r fix_pop_crack_pop/wireplumber/wireplumber.conf.d ~/.config/wireplumber
```

Restart audio

```
systemctl --user restart wireplumber pipewire pipewire-pulse
```

Restart your app (ex. Chrome). Done.

# Alternative: If pop/crack and audio cutting out persists

Copy Pipewire and Wireplumber config parts to /etc/

```
sudo cp -r fix_pop_crack_pop/pipewire /etc/
```
> [!NOTE]
> Wireplumber < 0.5
```
sudo cp -r fix_pop_crack_pop/wireplumber/main.lua.d /etc/wireplumber/
```
> [!NOTE]
> Modern Wireplumber ≥ 0.5
```
sudo cp -r fix_pop_crack_pop/wireplumber/wireplumber.conf.d /etc/wireplumber/
```


Restart Audio

```
systemctl --user restart wireplumber pipewire pipewire-pulse
```


Restart your app (ex. Chrome). Done.

### Special thanks

| User                                          |                                                                                      Description                                                                                        |
| :-------------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [lamperez](https://gist.github.com/lamperez)  | For [ACPI DSDT/SSDT patching guides](https://gist.github.com/lamperez/862763881c0e1c812392b5574727f6ff) and [tools](https://gist.github.com/lamperez/d5b385bc0c0c04928211e297a69f32d7)  |
| [thor2002ro](https://github.com/thor2002ro)   | For [GRUB patch](https://github.com/thor2002ro/asus_zenbook_ux3402za/tree/main/Sound) for similar laptop                                         |
