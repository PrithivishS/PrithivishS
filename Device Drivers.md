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


![image](https://github.com/user-attachments/assets/937ed17b-88be-47f5-8063-dd1423ff4a96)

Device major number #10 is unique as the kernel treats all the minor # beneath it as different devices. 

The new Linux Device Model
---------------------------
The new Linux Device Model, a bit simplistically ties to-getther these major components
- The buses on the system.
- The devices on them.
- The device drivers that drive the devices (Referred to also as client drivers)

** A fundamental LDM tenet is that every single device must reside on a bus. **

Once a device is succesfully enumerated or bound, then the kernel driver invokes the registered probe(). 
** Another Key aspect to understand regarding the LDM is that the modern LDM-based driver should typically do the following:
- Register itself to a (specialized) kernel framework.
- Register itself to a bus.

For e.g.
The kernel framework it registers itself to depends on the type of device you are working with;
for example,
- a driver for an RTC chip that resides on the I2C bus will register itself to the kernel's RTC framework (via the rtc_register_device() API) and to the I2C bus (internally via the i2c_register_driver() API). On the other hand,
-  a driver for a network adapter (a NIC) on the PCI bus will typically register itself to the kernel's network infrastructure (via the register_netdev() API) and the PCI bus (via the pci_register_driver() API).
-   Registering with a specialized kernel framework makes your job as a driver author a lot easier – the kernel will often provide helper routines (and even data structures) to take care of I/O details, and so on. For example, take the previously mentioned RTC chip driver.

You needn't know the details of how to communicate with the chip over the I2C bus, bit
banging out data on the Serial Clock (SCL)/Serial Data (SDA) lines as the I2C protocol
demands. The kernel I2C bus framework provides you with convenience routines (such as
the typically used **i2c_smbus_*() APIs**) that let you quite effortlessly communicate over
the bus to the chip in question!

Bus Driver Registration:To register with the bus driver, Device registers its following methods 
- Probe()
- Remove()
For devices that do **not reside on any physical bus** Linux kernel offers plafform bus (a pseudo bus infrastructure) registration. 
And for devices that do not pertain to any specialized subsystem infrastructure of the kernel, registering with the **kernel's misc framework** is the norm.

.fops = &llkd_misc_fops, /* connect to this driver's 'functionality' */

Without this above statement the device driver functionality cannot be invoked by a process that opens
/dev/miscdevice. Once a process gets a handle to the device driver it can now make calls to the other file operation functions. 

"If its not a process, it's a file." This is the central design principal of Unix and Linux 

Writing a MISC driver
---------------------




   


  

 

 







