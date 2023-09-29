# Demonstrate (LUKS)Linux Unified Key Setup on a Virtual Machine

- LUKS (Linux Unified Key Setup) is a disk encryption specification that provides a platform-independent standard on-disk format for use in various tools.
- It is a block device encryption that encrypts the entire block device and is therefore well-suited for protecting the contents of mobile devices such as removable storage media or laptop disk drives.
- LUKS establishes an on-disk format for the data, as well as a passphrase/key management policy.
- It uses the kernel device mapper subsystem via the `dm-crypt` module.
- The contents of the encrypted device are arbitrary, and therefore any file system can be encrypted, including swap partitions.
- LUKS uses a header to store metadata for encryption setup, which provides a generic key store on the dedicated area on a disk, with the ability to use multiple passphrases to unlock a stored key.
- LUKS2 has a more flexible way of storing metadata, which provides redundant information to provide recovery in the case of corruption in the metadata area.
- LUKS provides passphrase strengthening, which protects against dictionary attacks, and LUKS devices contain multiple key slots, which allows users to add backup keys or passphrases.
