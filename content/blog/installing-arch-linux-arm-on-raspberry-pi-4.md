+++
# Best practices from https://www.opengraph.xyz/: Keep title under 60 characters.
#        |----------------------------------------------------------|
title = "Installing 64-Bit Arch Linux for Arm on Raspberry Pi 4"

# Best practices from https://www.opengraph.xyz/: Keep description between 155 - 160 characters.
#              |---------------------------------------------------------------------------------------------------------------------------------------------------------|----|
description = "GitLab is currently the canonical \"source of truth\" for my personal Git repositories. This post shows how to automatically push them to GitHub using SSH deploy keys (and why you'd want to do it in the first place)."

# YYYY-MM-DD (2012-10-02) or RFC3339 (2002-10-02T15:00:00Z)
date = 2023-08-17
updated = 2023-08-17

draft = true
in_search_index = true

#[taxonomies]
#tags = ["ssh", "git", "github", "gitlab", "lock-in"]

# template = 
# weight = 
# slug = 
# path = 
# aliases = 
[extra]
+++


Go to https://archlinuxarm.org/platforms/armv8/broadcom/raspberry-pi-4

RPi 4 = Broadcom BCM2711 1.5GHz Quad Core ARMv8 Cortex-A72. I have 8 GB RAM

dmesg -wH and plug in SD card to get the device name. mine is /dev/sda

sudo fdisk /dev/sda

I want a GPT partition table and EFI booting so this is where my shit diverges from the official instructions

- **g** - create a new empty GPT partition table

Created a new GPT disklabel (GUID: 639B5AB8-CBF6-4C3A-A7A7-5A217165E991).
In red: The device contains 'dos' signature and it will be removed by a write command. See fdisk(8) man page and --wipe option for more details.

Oh no! Anyway...

- **n** - create a new partition
  - **1** (or nothing to accept the default) - the partition number 1
  - **2048** (or nothing to accept the default) - the first sector possible
  - https://wiki.archlinux.org/title/EFI_system_partition says at least 512 MB up to 1 GB. The author of gdisk http://www.rodsbooks.com/linux-uefi/ suggests 550 MiB. I have 32 GB SD card and probably won't fill it up. I'm going with 1 GB. so **+1G**. Created a new partition 1 of type 'Linux filesystem' and of size 1 GiB.
- **t** - change a partition type
  - Selected partition 1 automatically
  - **L** to see everything or **1** for EFI. Changed type of partition 'Linux filesystem' to 'EFI System'.
- Type n, then p for primary, 2 for the second partition on the drive, and then press ENTER twice to accept the default first and last sector. Created a new partition 2 of type 'Linux filesystem' and of size 28.1 GiB.
- Write the partition table and exit by typing w. 
- protip: https://stackoverflow.com/questions/12150116/how-to-script-sfdisk-or-parted-for-multiple-partitions
```bash
sudo sfdisk -d /dev/sda
label: gpt
label-id: 639B5AB8-CBF6-4C3A-A7A7-5A217165E991
device: /dev/sda
unit: sectors
first-lba: 2048
last-lba: 61069278
sector-size: 512

/dev/sda1 : start=        2048, size=     2097152, type=C12A7328-F81F-11D2-BA4B-00A0C93EC93B, uuid=4A993AA3-63ED-4BB9-BFA9-9B325EBBC5E6
/dev/sda2 : start=     2099200, size=    58968064, type=0FC63DAF-8483-4772-8E79-3D69D8477DE4, uuid=BE14AF11-7C09-4FFD-AE83-D35CDEC8C785
```
- sudo mkfs.fat -F 32 /dev/sda1
```bash
mkfs.fat 4.2 (2021-01-31)
```
- sudo mkfs.ext4 /dev/sda2
```bash
mke2fs 1.47.0 (5-Feb-2023)
/dev/sda2 contains `ISO-8859 text, with very long lines (65536), with no line terminators' data
Proceed anyway? (y,N) y
Creating filesystem with 7371008 4k blocks and 1843200 inodes
Filesystem UUID: d2a82aa4-2243-43c3-a6c8-0facb7026271
Superblock backups stored on blocks: 
	32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208, 
	4096000

Allocating group tables: done                            
Writing inode tables: done                            
Creating journal (32768 blocks): done
Writing superblocks and filesystem accounting information: done
```

I don't know what this means....
https://unix.stackexchange.com/questions/604019/malfunctioning-brand-new-usb

Oh no! Anyway...

sudo mkdir -p /mnt/arch64pi/boot
sudo mkdir -p /mnt/arch64pi/root

sudo mount /dev/sda1 /mnt/arch64pi/boot/
sudo mount /dev/sda2 /mnt/arch64pi/root/

Make sure to download the right tarball as well as hash and sigs
```
for ext in "" ".md5" ".sig"; do curl -L -o ~/Downloads/ArchLinuxARM-rpi-aarch64-latest.tar.gz$ext http://os.archlinuxarm.org/os/ArchLinuxARM-rpi-aarch64-latest.tar.gz$ext; done

-L is for fo**L**low redirects, -o is for **o**utput the file to this location
```

```
md5sum -c ArchLinuxARM-rpi-aarch64-latest.tar.gz.md5 
ArchLinuxARM-rpi-aarch64-latest.tar.gz: OK

-c for **c**heck
```

check signatures

https://archlinuxarm.org/about/package-signing

import the public key from https://archlinuxarm.org/about/package-signing

gpg2 --keyserver hkps://pgp.mit.edu/ --recv-keys 68B3537F39A313B3E574D06777193F152BDBE6A6

gpg: key 77193F152BDBE6A6: public key "Arch Linux ARM Build System <builder@archlinuxarm.org>" imported
gpg: Total number processed: 1
gpg:               imported: 1

gpg --verify ArchLinuxARM-rpi-aarch64-latest.tar.gz.sig ArchLinuxARM-rpi-aarch64-latest.tar.gz

gpg: Signature made Tue 28 Feb 2023 05:59:57 PM PST
gpg:                using RSA key 68B3537F39A313B3E574D06777193F152BDBE6A6
gpg: Good signature from "Arch Linux ARM Build System <builder@archlinuxarm.org>" [unknown]
gpg: WARNING: This key is not certified with a trusted signature!
gpg:          There is no indication that the signature belongs to the owner.
Primary key fingerprint: 68B3 537F 39A3 13B3 E574  D067 7719 3F15 2BDB E6A6

Good enough for me. 

Unpackage 

sudo bsdtar -xpf ArchLinuxARM-rpi-aarch64-latest.tar.gz -C /mnt/arch64pi/root

sudo sync

sudo mv /mnt/arch64pi/root/boot/* /mnt/arch64pi/boot

sudo umount /mnt/arch64pi/boot /mnt/arch64pi/root