https://cdn.amazonlinux.com/os-images/latest/virtualbox/

# Steps to create a base box

1. Download linux image for virtualbox in
[Latest image for virtualbox](https://cdn.amazonlinux.com/os-images/latest/virtualbox/)

2. Make a new virtual machine on virtualbox with type linux and version other linux (64-bit)

3. Select 'Use existing virtual disk' and point to image wich you download in step 1

4. After create virtual machine click on conf and in Storage add seed.iso present in this folder

5. Run box and login with user 'ec2-user' and password 'vagrant', if you logged as success shutdown the machiche to add 'Guest Additions'

6. Remove seed.iso and run again and login with 'ec2-user'

7. Update yum
```bash
sudo yum update
```

8. Add vagrant key
```bash
mkdir -p ~/.ssh
chmod 0700 ~/.ssh
wget --no-check-certificate https://raw.github.com/mitchellh/vagrant/master/keys/vagrant.pub -O ~/.ssh/authorized_keys
chmod 0600 ~/.ssh/authorized_keys
chown -R ec2-user ~/.ssh
```

9. In devices menu add 'Guest Additions image'

10. Install pre requirements
```bash
sudo yum install gcc-c++ make kernel-devel
```
11. Run the following commands
```bash
sudo mount -r -t iso9660 /dev/cdrom /media
cd /media
sudo ./VBoxLinuxAdditions.run
sudo systemctl enable vboxadd.service
```

12. Post processing (I do not know what that does)
```bash
export HISTSIZE=0
yum clean all
sudo rm -rf /var/cache/yum
sudo dd if=/dev/zero of=/ZERO bs=1M
sudo rm -f /ZERO
```

13. Shutdown the machine

14. Finally create a base box, in your terminal (not virtual machine) run
```bash
vagrant package --base {name_of_virtualbox_machine} --output {name_of_the_box}
```

Now you can deploy this box on vagrant cloud or add in your local vangrant boxes