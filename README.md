## Introduction

The repository provides Packer templates for unattended
building of relevant virtual machine images in the qcow2 format for
use with KVM and Nutanix AHV.


## Status

Currently the project includes templates Debian.Windows, CentOS and Ubuntu are in test phase.

Feel free to contribute more:-)

## Usage

### Build qcow2 image

Go into the relevant template directory and run packer build on the
relevant json file.

```bash
$ cd debian
$ export PACKER_LOG=1 && export PACKER_LOG_PATH="packer.log" && packer build debian96.json
```
After build the image you can share it with an http server.

## How to stage the builder
For build images for kvm you need a Qemu srver and Packer.

Here the procedure for setup an ubuntu 18.04 host for build images with packer.
```bash
apt-get update
apt-get install qemu-kvm unzip git
sudo apt-get install qemu-kvm libvirt-daemon-system libvirt-clients bridge-utils
kvm-ok
wget https://releases.hashicorp.com/packer/1.3.3/packer_1.3.3_linux_amd64.zip
unzip packer_1.3.3_linux_amd64.zip
mkdir /usr/local/packer
mv packer /usr/local/packer
cd /usr/bin
sudo ln -s /usr/local/packer/packer
source ~/.profile
```

Clone this repository
```
git clone https://github.com/DemisR/packer-qemu-templates.git
cd packer-qemu-templates/debian/
```

Share images with an Http server
```bash
apt install nginx
mkdir /var/www/vm-images/
```

Edit file `/etc/nginx/sites-enabled/default`
```
server {
  listen *:80;

  root /var/www/vm-images;
  autoindex on;
}
```

## Add images on Nutanix AHV
On Prism Central , go to Images services menu and Add Image.
Select URL source and type th path to your image ( ex : http://packer.mycompany.be/debian96-small.img ), click on Upload file .
Selecct Image Type : Disk , add the description and Save.

The conversion process take some minutes.

## Use images with nutanix
When you create a new Vm , remove the CD disk volume and add a new disk with the *operation* `clone from Image Service` and select the correct Image and add the netvork interface.

## Acknowledgements

* [packer-images](https://github.com/opentable/packer-images.git)
* [packer-windows](https://github.com/joefitzgerald/packer-windows)
* [box-cutter](https://github.com/boxcutter/)
