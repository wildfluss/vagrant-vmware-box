# How to create VMware (Fusion) Vagrant box

0.  Create VMware VM

    Add user vagrant with password vagrant

    Install `ifconfig` ,

        sudo visudo

    and add

        vagrant ALL=(ALL) NOPASSWD:ALL

1)  **install VMware Tools**

2)  Copy https://raw.githubusercontent.com/hashicorp/vagrant/master/keys/vagrant.pub to ~/.ssh/authorized_keys

3)  Create Full Clone and

        cd /path/to/Clone of foo.vmwarevm

4)  `/Applications/VMware\ Fusion.app/Contents/Library/vmware-vdiskmanager -d Virtual\ Disk.vmdk`

5)  `/Applications/VMware\ Fusion.app/Contents/Library/vmware-vdiskmanager -k Virtual\ Disk.vmdk`

6)  add `metadata.json` and create box

        cat <<EOF >./metadata.json
        {
          "provider": "vmware_desktop"
        }
        EOF

        tar cvzf foo.box ./*

7)  `vagrant box add foo-box foo.box`

8)  Check

        vagrant init foo-box

        vagrant up

    if you get

        ==> default: Cloning VMware VM: 'foo-box'. This can take some time...
        An error occurred while executing `vmrun`, a utility for controlling
        VMware machines. The command and output are below:

        Command: ["clone", "/Users/ysz/.vagrant.d/boxes/foo-box/0/vmware_desktop/foo.vmx", "/Users/ysz/foo-box/.vagrant/machines/default/vmware_desktop/0ddc9f14-3e4c-44ab-a535-0aae6c6358a2/foo.vmx", "linked", {:notify=>[:stdout, :stderr]}]

        Stdout: Error: The file is already in use

    then add this to `Vagrantfile`

        config.vm.provider 'vmware_fusion' do |p|
          p.linked_clone = false
        end

    or Create and use Full Clone of VM ^^

    if you get

        ==> default: Machine booted and ready!
        ==> default: Configuring network adapters within the VM...
        The following SSH command responded with a non-zero exit status.
        Vagrant assumes that this means the command failed!

        /sbin/ip -o -0 addr | grep -v LOOPBACK | awk '{print $2}' | sed 's/://'

        Stdout from the command:


        Stderr from the command:

    ignore it and try `vagrant ssh` again

6.  Upload New Version to

        https://app.vagrantup.com/ysz/boxes/foo
