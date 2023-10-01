# Demonstrate (LUKS)Linux Unified Key Setup on a Virtual Machine

## Introduction

- LUKS (Linux Unified Key Setup) is a disk encryption specification that provides a platform-independent standard on-disk format for use in various tools.
- It is a block device encryption that encrypts the entire block device and is therefore well-suited for protecting the contents of mobile devices such as removable storage media or laptop disk drives.
- It uses the kernel device mapper subsystem via the `dm-crypt` module.
- The contents of the encrypted device are arbitrary, and therefore any file system can be encrypted, including swap partitions.
- LUKS uses a header to store metadata for encryption setup, which provides a generic key store on the dedicated area on a disk, with the ability to use multiple passphrases to unlock a stored key.
- LUKS provides passphrase strengthening, which protects against dictionary attacks, and LUKS devices contain multiple key slots, which allows users to add backup keys or passphrases.

## Overview of LUKS
### What LUKS does:
- **LUKS encrypts entire block devices**
  - LUKS is thereby well-suited for protecting the contents of mobile devices such as:
    - Removable storage media
    - Laptop disk drives

  - The underlying contents of the encrypted block device are arbitrary.
    - This makes it useful for encrypting swap devices.
    - This can also be useful with certain databases that use specially formatted block devices for data storage.

  - LUKS uses the existing device mapper kernel subsystem.
    - This is the same subsystem used by LVM, so it is well tested.

  - LUKS provides passphrase strengthening.
    - This protects against dictionary attacks.

  - LUKS devices contain multiple key slots.
    - This allows users to add backup keys/passphrases.

  - What LUKS does not do:
    - LUKS is not well-suited for applications requiring many (more than eight) users to have distinct access keys to the same device.
    - LUKS is not well-suited for applications requiring file-level encryption.

## Steps to demonstrate LUKS on VM
1. Create a new virtual machine with a blank disk.
2. Install the operating system on the virtual machine.
3. Install the LUKS packages on the virtual machine using `apt-get install cryptsetup` or `sudo apt install cryptsetup` if not installed.
4. Partition the virtual disk and format the partitions.
5. Encrypt the partition with LUKS using the `cryptsetup` command.
6. Mount the encrypted partition and enter the password to unlock it.
7. Use the encrypted partition as desired.

## Frequently used `cryptsetup` commands
1. Initialize a LUKS-encrypted Volume:
  - `sudo cryptsetup luksFormat /dev/sdX`
  - This command initializes a LUKS header on the specified block device /dev/sdX and sets up a passphrase or encryption key.
  
  
2. Open a LUKS-encrypted Volume:
  - `sudo cryptsetup luksOpen /dev/sdX mapped_name`
  - This command unlocks (opens) a LUKS-encrypted volume located on /dev/sdX and maps it to a device with the name mapped_name.
  

3. Close (Lock) a LUKS-encrypted Volume:
  - `sudo cryptsetup luksClose mapped_name`
  - This command closes (locks) an open LUKS-encrypted volume that was previously mapped as mapped_name.
 

4. Add a New Passphrase or Key:
  - `sudo cryptsetup luksAddKey /dev/sdX`
  - This command allows you to add a new passphrase or encryption key to a LUKS-encrypted volume.
 
  
5. Change a Passphrase or Key:
  - `sudo cryptsetup luksChangeKey /dev/sdX`
  - Use this command to change an existing passphrase or encryption key for a LUKS-encrypted volume.
 
  
6. Remove a Passphrase or Key:
  - `sudo cryptsetup luksRemoveKey /dev/sdX`
  - This command lets you remove an existing passphrase or encryption key from a LUKS-encrypted volume.
 
  
7. Check LUKS Status:
  - `sudo cryptsetup luksDump /dev/sdX`
  - This command provides detailed information about the LUKS header and the status of a LUKS-encrypted volume.

## Advantages and Limitations of LUKS Encryption on a Virtual Machine
### Advantages:
  - Provides a high level of security for your data
  - Allows you to encrypt your data without having to purchase expensive hardware
  - Is easily configurable and can be used with a variety of different operating systems

### Disadvantages:
  - Can be resource-intensive and may slow down the performance of your system
  - If you lose your encryption key, **you will not be able to recover the data** on your storage device

### Conclusion:
In summary, LUKS is a reliable and well-tested disk encryption specification that provides a high level of security for your data. It encrypts the entire block device and is well-suited for protecting the contents of mobile devices such as removable storage media or laptop disk drives. LUKS uses a header to store metadata for encryption setup, which provides a generic key store on the dedicated area on a disk, with the ability to use multiple passphrases to unlock a stored key. LUKS provides passphrase strengthening, which protects against dictionary attacks, and LUKS devices contain multiple key slots, which allows users to add backup keys or passphrases. However, LUKS is not well-suited for applications requiring many (more than eight) users to have distinct access keys to the same device, and it is not well-suited for applications requiring file-level encryption.


### References:
  - [Linux Unified Key Setup](https://en.wikipedia.org/wiki/Linux_Unified_Key_Setup)
  - [Red Hat Enterprise Linux](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/security_hardening/encrypting-block-devices-using-luks_security-hardening)
  - [Disk Encryption User Guide](https://docs.fedoraproject.org/en-US/quick-docs/encrypting-drives-using-LUKS/)
  - [How To Use LUKS Utility in Linux For Disk Encryption](https://youtube.com/watch?v=nWQB-Wq8V8I)
  - [How To Use Linux LUKS Full Disk Encryption For Internal / External / Boot Drives](https://youtube.com/watch?v=5rlZtasM-Pk&t=0)

---
*Project By Robin Rajesh & Rhea Yadav*
