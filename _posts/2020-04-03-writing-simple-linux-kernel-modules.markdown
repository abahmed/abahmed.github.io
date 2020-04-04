---
layout: post
title:  Writing Simple Linux Kernel Modules
description: Write your first Linux Kernel module
date:   2020-04-04 21:00:00 +0200
categories: Linux Kernel
tags: linux kernel module c development lkm extension introduction hello world ubuntu headers make ko rmmod insmod modinfo debian mint
permalink: /article/:title
comments: true
uuid: 080f2106-f03d-4941-9555-547e4378ef33
---
**Linux Kernel Modules** (LKM) (called `kernel extension` in other operating systems) are pieces of code that can be loaded and unloaded into the kernel upon demand. Here I'm going to guide you write your first linux kernel module. 

Through modules you can extend kernel functionalities without rebooting the system. This is powerful as you don't have to rebuild and reboot the kernel to add new functionalities.

## What are LKMs used for?
LKMs give you accessibility to system hardware since your code will be part of the kernel and that enables you to do a lot (be careful as you can crash the system easily). For example
 - Device Drivers
 - Network Drivers
 - File System Drivers
 - System Calls

## Write Hello World Kernel Module
Now, we are going to write a simple kernel module that prints a `Hello World!` message when it's loaded and `Good Bye World!` when it's unloaded.

### Installing the linux headers

#### Debian based distributions (Debian / Ubuntu / Linux Mint / elementary OS)
```bash
sudo apt install -y build-essential linux-headers-$(uname -r) make libelf-dev
```
- `$(uname -r)` gets current kernel release

### Module Source Code

Create file `hello-world.c`
```c
/*  
 *  hello-world.c
 */
#include <linux/module.h>	/* Needed by all modules */
#include <linux/kernel.h>	/* Needed for KERN_INFO */

MODULE_LICENSE("GPL");
MODULE_AUTHOR("Abdelrahman Ahmed");
MODULE_DESCRIPTION("Hello World module");

int init_module(void)
{
	printk(KERN_INFO "Hello World!\n");

	/* 
	 * On success, return 0.
	 * On error, return -1 and errno is set according to error
	 */
	return 0;
}

void cleanup_module(void)
{
	printk(KERN_INFO "Good Bye World!\n");
}
```
`printk` (defined in kernel) prints messages to the kernel log and has an optional prefix string `Loglevel` indicates priority of that message. In previous example we set logging level to `KERN_INFO` (Normal information)

### Compile Kernel Module
Kernel modules is compiled differently from usual programs. You need to create a `Makefile`(**case sensitive**) in the same directory of our module `hello-world.c`

```makefile
obj-m += hello-world.o

all:
	make -C /lib/modules/$(shell uname -r)/build M=$(PWD) modules

clean:
	make -C /lib/modules/$(shell uname -r)/build M=$(PWD) clean
```

This file simply compiles `hello-world` module and this is a simple explanation for this file
- Targets `all` and `clean` are required for makefiles to build and clean your module
- `$(shell uname -r)` gets current kernel release
- `$(PWD)` gets current directory
- Make calls `Makefile` of kernel's builder (`-C` changes to that path) and sets a variable `M` to return to your current directory after processing it

```bash
ab@ubuntu:~/hello-world$ make 
make -C /lib/modules/4.15.0/build M=/home/ab/hello-world modules
make[1]: Entering directory '/usr/src/linux-headers-4.15.0'
  CC [M]  /home/ab/hello-world/hello-world.o
  Building modules, stage 2.
  MODPOST 1 modules
  CC      /home/ab/hello-world/hello-world.mod.o
  LD [M]  /home/ab/hello-world/hello-world.ko
make[1]: Leaving directory '/usr/src/linux-headers-4.15.0'
```

Now, we have built our first kernel module. you will find it in current directory with name `hello-world.ko`. Let's get more info about this module by executing `modinfo hello-world.ko`
```bash
ab@ubuntu:~/hello-world$ modinfo hello-world.ko
filename:       /home/ab/hello-world/hello-world.ko
description:    Hello World module
author:         Abdelrahman Ahmed
license:        GPL
srcversion:     5A77F42048F97F6D685FF74
depends:        
retpoline:      Y
name:           hello_world
vermagic:       4.15.0 SMP mod_unload 
```

### Load Kernel Module

To **load** kernel module, you just need to execute command `sudo insmod hello-world.ko`. 

When module is inserted into kernel, the `init_module` will be invoked

After **loading** Hello World module, let's check our **loading** message in kernel log by executing `dmesg | tail -1` (getting only last message)
```bash
ab@ubuntu:~/hello-world$ dmesg | tail -1
[2753755.444706] Hello World!
```

### Unload Kernel Module

To **unload** kernel module, you just need to execute command `sudo rmmod hello-world.ko`. 

when the module is removed from kernel, the `cleanup_module` will be invoked

After **unloading** it, let's check our **unloading** message in kernel log by executing `dmesg | tail -1` again
```bash
ab@ubuntu:~/hello-world$ dmesg | tail -1
[2753926.708205] Good Bye World!
```

**Finally**, you wrote your first Linux Kernel Module :tada: and be able to load and unload it. Hopefully, this article is helpful for you. If you have any question ask in comments. Thanks for reading :heart:
