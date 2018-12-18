# Genate base box image

1. Download linux image for virtualbox in
[Latest image for virtualbox](https://cdn.amazonlinux.com/os-images/latest/virtualbox/)

2. Make a new virtual machine on virtualbox with name 'aml2', type linux and version other linux (64-bit)

3. Select 'Use existing virtual disk' and point to image wich you download in step 1

4. After create virtual machine click on conf and in Storage add seed.iso present in this folder

5. Run box and login with user 'ec2-user' and password 'vagrant'.

6. Shutdown the machine.

7. Finally create a base box, in your terminal (not virtual machine) run
```bash
vagrant package --base aml2 --output aml2.box
```

8. Add it in your box list
```base
vagrant box add aml2 --name=aml2
```

## If need generate a new seed.iso
run
```bash
genisoimage -output seed.iso -volid cidata -joliet -rock user-data meta-data
```
