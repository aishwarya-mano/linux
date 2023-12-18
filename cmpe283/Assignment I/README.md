# Team Composition
- **Aishwarya Manoharan**
- **Sanjay Sathyarapu**

# Contributions
- **Aishwarya:** Orchestrated the setup for Assignment 1 on a GCP instance and developed the code for both tertiary and secondary procbased structures.
- **Sanjay:** Focused on researching exit controls following the Software Developer Manual (SDM) guidelines and played a key role in coding entry and exit structures, as well as procbased controls.

# Implementation Steps

1. Fork Linux Kernel Repository:
   Begin by forking the Linux kernel repository from `https://github.com/torvalds/linux` into your GitHub account to create your own copy of the source code.

2. Install Dependencies on GCP:
   On your GCP instance, execute the following command to install necessary dependencies:

   $ sudo apt-get install libncurses-dev gawk flex bison openssl libssl-dev dkms libelf-dev libudev-dev libpci-dev libiberty-dev autoconf llvm
   


3. Install Dependencies on GCP:

   $ git clone https://github.com/aishwarya-mano/linux.git


4. Set Up and Modify cmpe283-1.c

   $ cd linux
   
   $ cp /boot/[your version] .config



6. Compile the code:

   $ make



7. Load the Module and Verify Changes:

   $ sudo insmod cmpe283-1.ko
   
   $ dmesg


Upon finishing these steps, you will be in a position to examine the VMX functionalities of every Model Specific Register (MSR) present in the system.
