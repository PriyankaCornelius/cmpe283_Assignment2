# cmpe283_Assignment2

ANSWER 2-

1) Clone the torvalds/linux Git repository:

git clone https://github.com/torvalds/linux.git

2) Build the Kernel:

sudo bash

apt-get install build-essential kernel-package fakeroot libncurses5-dev libssl-dev ccache bison flex libelf-dev

uname -a (and note down your kernel version, for example “5.4.0-52-generic”)

cp /boot/config-4.15.0-112-generic ./.config (substitute your version obtained from the previous step here though)

make oldconfig (and then just use the default for everything, don’t change anything – you can do this by holding down enter)

make && make modules && make install && make modules-install (will take a long time the first time)

reboot

3) Verify that you are using the newer kernel (5.8, etc) after reboot:

uname -a (In my case version after reboot is 5.10.0-rc1)

4) dd the code for calculating total number of exits and the total time spent processing all exits in cpuid.c and vmx.c

Modified functions:- kvm_emulate_cpuid in linux/arch/x86/kvm/cupid.c, and vmx_handle_exit in linux/arch/x86/kvm/vmx/vmx.c

5) Build the updated code

sudo make -j 2 modules M=arch/x86/kvm 

6) Load and unload the kvm kernel object "kvm.ko" and kvm-intel module "kvm-intel.ko" :

sudo rmmod arch/x86/kvm/kvm-intel.ko

sudo rmmod arch/x86/kvm/kvm.ko

sudo insmod arch/x86/kvm/kvm.ko

sudo insmod arch/x86/kvm/kvm-intel.ko

7) Create a VM using virt manager:

sudo apt-get update

sudo apt install qemu-kvm libvirt-daemon-system libvirt-clients bridge-utils virt-manager 

8) Verify KVM Installation using the following command. You should see an empty list of virtual machines which indicates that everything is working correctly.

virsh -c qemu:///system list

9) Create inner nested VM inside the virtual machine manager using Ubuntu ISO file:

10) Install cpuid in the inner VM:

sudo apt-get update

sudo apt-get install cpuid

11) Create test program name - Test_Assignment2.c inside inner vm

12) Compile Test_Assignment2.c using gcc :

gcc Test_Assignment2.c-o test

13) Run test1 executable file on terminal:

./test



ANSWER 3-

After execution of each test, the number of exits are increasing.

The number of exits does not increase at a stable rate.

More exits occur during certain VM operations like I/O instructions.

In a full VM boot, more than 2000000 exits occur.
