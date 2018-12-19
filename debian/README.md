# Debian images QEMU

## Debian 9.6

OS : Debain 9.6
Packages :
  - curl
  - htop
  - ntp
  - rsync
  - sudo
  - vim
  - cloud-init

Partitioning:
Single disk with LVM partitioning and ext4 partitions.
  - Boot: 256MB
  - Root: At least 4GB, will fill to the end of the disk
  - Var: 4GB
