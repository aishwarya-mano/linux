Steps to setup the Environment:

Obtain the Linux Kernel Source Code:

$ git clone https://github.com/aishwarya-mano/linux.git

Navigate to the Linux directory:

$ cd linux


Install the required packages:

apt-get install build-essential kernel-package fakeroot libncurses5-dev libssl-dev ccache bison flex libelf-dev 
Copy the Boot Config file to the Linux folder:

$ sudo bash && cp /boot/config-[your VM version] .config

Perform an old configuration:

$ make oldconfig

Build the kernel image:

$ make prepare && make -j[# of CPUs on your VM]

Build kernel modules:

$ make -j8 modules

Install modules ( Update the command):

$ sudo make INSTALL_MOD_STRIP=1 modules_install && sudo make install

Reboot the system:

$ reboot

Verify the kernel module changes:

$ uname -a

 Download the necessary tools for hosting a nested VM:

$ sudo apt-get install qemu-kvm libvirt-bin virtinst bridge-utils cpu-checker

 Install a Linux ISO image of your choice (We selected CentOS):

Download CentOS ISO:
$ wget "https://centos.mirror.shastacoe.net/centos/7.9.2009/isos/x86_64/CentOS-7-x86_64-Minimal-2207-02.iso"

Update KVM and KVM_INTEL modules:
$ rmmod kvm_intel && rmmod kvm && modprobe kvm && modprobe kvm_intel && lsmod | grep kvm

Create the nested VM:

$ virt-install --network bridge:virbr0 --name nested-vm --os-variant=centos7.0 --ram=2048 --vcpus=2 --disk size=20 --graphics none --location=[your_path] --extra-args="console=tty0 console=ttyS0,115200" --check all=off

Start the VM and access the console:

$ virsh start [your VM name]
$ virsh console [your VM name]
$ virsh shutdown [your VM name]
