# Environment Setup Guide

This guide provides step-by-step instructions for setting up your environment.

## Getting the Linux Kernel Source

1. **Clone the Linux Kernel Repository:**
    ```bash
    git clone https://github.com/aishwarya-mano/linux.git
    ```

2. **Navigate to the Linux Directory:**
    ```bash
    cd linux
    ```

3. **Install the Required Packages:**
    ```bash
    apt-get install build-essential kernel-package fakeroot libncurses5-dev libssl-dev ccache bison flex libelf-dev
    ```

4. **Copy the Boot Config File to the Linux Folder:**
    Replace `("Your_VM_Version")` with your actual VM version.
    ```bash
    cp /boot/config-("Your_VM_Version") .config
    ```

5. **Make Old Configuration:**
    ```bash
    make oldconfig
    ```

6. **Build Kernel Modules:**
    ```bash
    make -j 8 modules
    ```

7. **Build the Kernel Image:**
    ```bash
    make prepare
    make -j 8
    ```

8. **Install the Modules:**
    ```bash
    sudo make INSTALL_MOD_STRIP=1 modules_install && sudo make install
    ```

9. **Reboot the VM:**
    ```bash
    reboot
    ```

10. **Verify the Kernel Module Name Change:**
    ```bash
    uname -a
    ```

11. **Download the Required Tools for Hosting a Nested VM:**
    ```bash
    sudo apt-get install qemu-kvm libvirt-bin virtinst bridge-utils cpu-checker
    ```

12. **Install a Linux ISO Image of Your Choice:**
    For this setup, CentOS was selected. You can download it using the following command, or replace the URL with the ISO of your preferred Linux distribution.
    ```bash
    wget "https://centos.mirror.shastacoe.net/centos/7.9.2009/isos/x86_64/CentOS-7-x86_64-Minimal-2207-02.iso"
    ```

13. **Remove the KVM and KVM_INTEL Modules:**
    ```bash
    rmmod kvm_intel
    rmmod kvm
    ```
14. **Update the KVM and KVM_INTEL Modules:**
    ```bash
    modprobe kvm
    modprobe kvm_intel
    lsmod | grep kvm
    ```

15. **Create the Nested VM:**
    Replace `[your_path]` with the path to your CentOS ISO.
    ```bash
    virt-install --network bridge:virbr0 --name centosvm2 --os-variant=centos7.0 --ram=2048 --vcpus=2 --disk size=20 --graphics none --location=[your_path] --extra-args="console=tty0 console=ttyS0,115200" --check all=off
    ```

16. **Start the VM and Enter the Console:**
    ```bash
    virsh start centosvm2
    virsh console centosvm2
    virsh shutdown centosvm2
    ```
