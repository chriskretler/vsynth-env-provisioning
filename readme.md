################
## Packer ######
################
# packer comes as a pre-built binary:
https://www.packer.io/downloads.html
After extracting:
$ sudo mv /storage/builds/packer /usr/local/bin
$ packer -version
1.5.1

# To build a vagrant box:
$ git clone https://github.com/boxcutter/ubuntu
$ cd ubuntu

$ packer build -var-file=ubuntu1804-desktop.json ubuntu.json
...
--> virtualbox-iso: 'virtualbox' provider box: box/virtualbox/ubuntu1804-desktop-0.1.0.box

$ sudo find / -type f -iname *.box
/storage/code/ubuntu/box/virtualbox/ubuntu1804-desktop-0.1.0.box

################
## Vagrant #####
################
#To install vagrant:
sudo apt install vagrant

# Add packer image
$ vagrant box add /storage/code/ubuntu/box/virtualbox/ubuntu1804-desktop-0.1.0.box --name=ubuntu1804-desktop
==> box: Box file was not detected as metadata. Adding it directly...
==> box: Adding box 'ubuntu1804-desktop' (v0) for provider: 
    box: Unpacking necessary files from: file:///storage/code/ubuntu/box/virtualbox/ubuntu1804-desktop-0.1.0.box
==> box: Successfully added box 'ubuntu1804-desktop' (v0) for 'virtualbox'!

# Verify added image
$ vagrant box list
ubuntu1804-desktop (virtualbox, 0)

# To create:
vagrant up

# To test changes from beginning:
vagrant destroy
vagrant up

# To test for idempotency
vagrant reload --provision-with shell

# To shut-down a vagrant machine
vagrant halt