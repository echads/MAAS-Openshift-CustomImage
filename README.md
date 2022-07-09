Create custom image from Openshift Assisted Installer ISO
===============================

Prepare your custom Image Environnement
------------------
```bash
wget -O- https://apt.releases.hashicorp.com/gpg | gpg --dearmor | sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg
```
```bash
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
```
```bash
sudo apt update && sudo apt install -y packer qemu-utils bridge-utils cpu-checker libvirt-clients libvirt-daemon qemu qemu-kvm
```

```bash
git clone https://github.com/canonical/packer-maas.git
```

Building an image
------------------
```bash
cd packer-maas/rhel8/ && make ISO=/PATH/TO/file.iso
```

Uploading an image to MAAS
---------------
```bash
maas url boot-resources create name='rhel/openshift' title='Openshift Assisted Installer' architecture='amd64/generic' filetype='tgz' content@=rhel8.tar.gz
```
