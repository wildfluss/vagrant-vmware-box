# myvagrant

0. create VMware VM

1. **install VMware Tools**

2. copy https://raw.githubusercontent.com/hashicorp/vagrant/master/keys/vagrant.pub to ~/.ssh/authorized_keys

3. cd /path/to/foo/.vagrant/machines/default/vmware_fusion/blah

4. /Applications/VMware\ Fusion.app/Contents/Library/vmware-vdiskmanager -d Virtual\ Disk.vmdk

5. /Applications/VMware\ Fusion.app/Contents/Library/vmware-vdiskmanager -k Virtual\ Disk.vmdk

3. tar cvzf foo.box ./*

4. vagrant box add foo-box foo.box

5. check

        vagrant init foo-box
        
        vagrant up 

6. upload New Version to

        https://app.vagrantup.com/ysz/boxes/foo

