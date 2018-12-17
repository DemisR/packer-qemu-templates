# Packer installation

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


# Create ubuntu image

cd
git clone https://github.com/DemisR/packer-qemu-templates.git
cd packer-qemu-templates/debian/
export PACKER_LOG=1 && export PACKER_LOG_PATH="packer.log" && packer build debian96.json
cp output_image/debian96-small.img /var/www/vm-images

# On Nutanig interface
create new iage based on url http://10.22.120.249/debian96-small.img
