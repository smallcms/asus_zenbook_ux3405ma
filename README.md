# ASUS Zenbook UX3405MA amplifier
SSDT Patch to fix missing speakers sound on Asus Zenbook 14 UX3405MA (2024) and latest BIOS

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

### build the _ssdt-csc3551.dsl_

```
iasl -tc ssdt-csc3551.dsl
```

### copy it in /boot

```
sudo cp -f ssdt-csc3551.aml /boot
```

### copy grub script

```
sudo cp -f 01_acpi /etc/grub.d && sudo chmod +x /etc/grub.d/01_acpi
```

### update grub config

* Update grub config
  * Debian / Ubuntu based distributions

    ```sudo update-grub```

  * Fedora / RHEL-based distributions

    ```sudo grub2-mkconfig -o /etc/grub2.cfg```

    ```sudo grub2-mkconfig -o /etc/grub2-efi.cfg```

  * Arch based distributions

    ```grub-mkconfig -o /boot/grub/grub.cfg```

### reboot

### Special thanks

| User                                          |                                                                                      Description                                                                                        |
| :-------------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [lamperez](https://gist.github.com/lamperez)  | For [ACPI DSDT/SSDT patching guides](https://gist.github.com/lamperez/862763881c0e1c812392b5574727f6ff) and [tools](https://gist.github.com/lamperez/d5b385bc0c0c04928211e297a69f32d7)  |
| [thor2002ro](https://github.com/thor2002ro)   | For [GRUB patch](https://github.com/thor2002ro/asus_zenbook_ux3402za/tree/main/Sound) for similar laptop                                         |
