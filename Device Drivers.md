Driver Methods
---------------

A device driver provides several entry points into the kernel. These are **file related system calls** known as drivers' methods. 
So, we can have an 
open() method,
a read() method,
a write() method, 
an llseek() method,
an [unlocked|compat]_ioctl() method,
a release() method, and so on. 

Refer to **structure: include/linux/fs.h:file_operations**

Defintion of Device driver: A device is the interface between the OS and a peripheral device. It can be written inline - that is compiled within the kernel image file OR 
more commonly outside of the kernel source tree as a kernel module. 

In order for a user space application to gain access to the underlying device driver within the kernel, some I/O mechanism is required. The Unix (Linux) design is to
have  the process open a special type of file  - a **device file, or device node**. This files typically live in the /dev directory, and on modern systems are dynamic and auto populated. 
The device node serves as an entry point into the device driver.

In order for the kernel to distinguish between device files, it uses two attributes within their intode data structure:
- The type of file - either character (char) or block 
- The manjor and minor number. 

The Device Namespace
---------------------
The device type and  the {major #, minor #} pair form a hierarchy.  Devices (and thus their drivers) are organized within a tree-like hierarchy with the kernel. 
The hierarchy is first divided based on device type - block or char. Within that, we have some n major numbers for each type, and each major number is further classified
via some m minor numbers. 






