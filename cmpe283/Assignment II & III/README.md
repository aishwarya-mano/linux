# Environment Setup Guide

This guide provides step-by-step instructions for setting up your environment.

# Team Members:
1. Aishwarya Manoharan
2. Sanjay Sathyarapu

## Steps on getting the Linux Kernel Source

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
## Questions

### Assignment #2 (0x4FFFFFFF) & (0x4FFFFFFD)

* **Contribution**
   
  * Aishwarya - Completed the setup for the nested VM environment and executed coding for leaf node 0x4FFFFFFD.
  * Sanjay - Executed code development for leaf node 0x4FFFFFFF, crafted the testing program, and verified the correctness of the outcomes

* **Describe in detail the steps you used to complete the assignment.**
    *  Please find the above steps.
   
### Assignment #3 (0x4FFFFFFC) & (0x4FFFFFFE)

* **Contribution**
    * Aishwarya - Completed the environment setup for the nested VM and implemented the code for leaf node 0x4FFFFFFC.
    * Sanjay - Executed the coding for leaf node 0x4FFFFFFE, formulated and tested the program, ensuring result accuracy, and collaborated with Aishwarya in verifying the outcomes for the assignment questions.

* **Describe in detail the steps you used to complete the assignment.**
    * Please read the steps mentioned above

* **Comment on the frequency of exits – does the number of exits increase at a stable rate? Or are there more exits performed during certain VM operations? Approximately how many exits does a full VM boot entail?**
    * The frequency of exits is irregular, with varying counts for different exit numbers.
    * The total number of exits during a full VM boot appears contradictory, as it decreases from 1,201,533 to 0.
   
* **Of the exit types defined in the SDM, which are the most frequent? Least?**
    * The most frequent exit for us is exit number 30, with total exits as 1510473
    * The Least was 29 and 55, with 5 total exits.
    * There were many exit numbers with 0 exits.

### Output screenshots
* **Leaf node 0X4FFFFFFF**
  ![](/images/0x4fffffff.jpeg??raw=true "Optional Title")
  ![Alt text](/images/dmesg_0x4fffffff.jpeg?raw=true "Optional Title")
  
* **Leaf node 0X4FFFFFFC**
   ![Alt text](/images/0x4ffffffc.jpeg?raw=true "Optional Title")
   ![Alt text](/images/dmesg_0x4ffffffc.jpeg?raw=true "Optional Title")

* **Leaf node 0X4FFFFFFD**
   ![Alt text](/images/0x4ffffffd.jpeg??raw=true "Optional Title")
   ![Alt text](/images/dmesg_0x4ffffffd.jpeg?raw=true "Optional Title")

* **Leaf node 0X4FFFFFFE**
   ![Alt text](/images/0x4ffffffe.jpeg??raw=true "Optional Title")
   ![Alt text](/images/dmesg_0x4ffffffe.jpeg?raw=true "Optional Title")
   
