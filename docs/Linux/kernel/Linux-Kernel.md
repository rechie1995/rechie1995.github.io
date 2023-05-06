# 什么是Linux内核

## Linux内核概述

Linux内核是Linux操作系统的主要组件，也是计算机硬件与其进程之间的核心接口。它负责两者之间的通信，还要尽可能高效地管理资源。

之所以称为内核，是因为它在操作系统中就像果实硬壳中的种子一样，并且控制着硬件（无论是手机、笔记本电脑、服务器，还是任何其他类型的计算机）的所有主要功能。

内核包安装在`/usr/lib/modules/`路径下，并随后用于生成储存在`/boot/`中的可执行镜像。为了能够启动到内核，需要正确配置启动加载器。

## 内核的作用是什么？

内核有四项工作：

- 内存管理：追踪记录有多少内存存储了什么以及存储在哪里
- 进程管理：确定哪些进程可以使用CPU、何时使用以及持续多长时间
- 设备驱动程序：充当硬件与进程之间的调解程序/解释程序
- 系统调用和安全防护：从流程接受服务请求

## 内核的整体架构和子系统

内核提出了5个子系统，分别负责如下的功能：

- Process Scheduler，也称作进程管理、进程调度。负责管理CPU资源，以便让各个进程可以用尽量公平的方式访问CPU。
- Memory Manager，内存管理。负责管理内存资源，以便让各个进程可以安全地共享机器的内存资源。另外，内存管理会提供虚拟内存的机制，该机制可以让进程使用多于系统可用的内存，不用的内存会通过文件系统保存在外部非易失存储器中，需要使用的时候，再取回到内存中。
- VFS(Virtual File System)，虚拟文件系统。Linux内核将不同功能的外部设备，例如Disk设备(硬盘、磁盘、NAND Flash、Nor Flash等)、输入输出设备、显示设备等等，抽象为可以通过统一的文件操作接口(open、close、read、write等)来访问。这就是Linux系统“一切皆是文件”的体现。
- Network，网络子系统。负责管理系统的网络设备，并实现多种多样的网络标准。
- IPC，进程间通信。IPC不管理任何的硬件，它主要负责Linux系统中进程之间的通信。

## 内核源代码的目录结构

- include/ ---- 内核头文件，需要提供给外部模块（例如用户空间代码）使用。
- kernel/ ---- Linux内核的核心代码，包含了进程调度子系统，以及和进程调度相关的模块。
- mm/ ---- 内存管理子系统。
- fs/ ---- VFS子系统。
- net/ ---- 不包括网络设备驱动的网络子系统。
- ipc/ ---- IPC（进程间通信）子系统。
- arch// ---- 体系结构相关的代码，例如arm, x86等等。
- arch//mach- ---- 具体的machine/board相关的代码。
- arch//include/asm ---- 体系结构相关的头文件。
- arch//boot/dts ---- 设备树（Device Tree）文件。
- init/ ---- Linux系统启动初始化相关的代码。
- block/ ---- 提供块设备的层次。
- sound/ ---- 音频相关的驱动及子系统，可以看作“音频子系统”。
- drivers/ ---- 设备驱动（在Linux kernel 3.10中，设备驱动占了49.4的代码量）。
- lib/ ---- 实现需要在内核中使用的库函数，例如CRC、FIFO、list、MD5等。
- crypto/ ----- 加密、解密相关的库函数。
- security/ ---- 提供安全特性（SELinux）。
- virt/ ---- 提供虚拟机技术（KVM等）的支持。
- usr/ ---- 用于生成initramfs的代码。
- firmware/ ---- 保存用于驱动第三方设备的固件。
- samples/ ---- 一些示例代码。
- tools/ ---- 一些常用工具，如性能剖析、自测试等。
- Kconfig, Kbuild, Makefile, scripts/ ---- 用于内核编译的配置文件、脚本等。
- COPYING ---- 版权声明。
- MAINTAINERS ----维护者名单。
- CREDITS ---- Linux主要的贡献者名单。
- REPORTING-BUGS ---- Bug上报的指南。
- Documentation, README ---- 帮助、说明文档。

## 内核配置

- `make config`       纯文本界面。
- `make menuconfig`   基于文本的彩色菜单、选项列表和对话框。
- `make nconfig`      增强的基于文本的彩色菜单。
- `make xconfig`      基于Qt的配置工具。
- `make gconfig`      基于GTK+的配置工具。
- `make oldconfig`    基于现有的 ./.config 文件选择所有选项，并询问新配置选项。
- `make olddefconfig` 类似上一个，但不询问直接将新选项设置为默认值。
- `make defconfig`    根据体系架构，使用arch/$arch/defconfig或arch/$arch/configs/${PLATFORM}_defconfig中的默认选项值创建./.config文件。
- `make ${PLATFORM}_defconfig` 使用arch/$arch/configs/${PLATFORM}_defconfig中的默认选项值创建一个./.config文件。用`make help`来获取您体系架构中所有可用平台的列表。
- `make allyesconfig` 通过尽可能将选项值设置为“y”，创建一个./.config文件。
- `make allmodconfig` 通过尽可能将选项值设置为“m”，创建一个./.config文件。
- `make allnoconfig`  通过尽可能将选项值设置为“n”，创建一个./.config文件。
- `make randconfig`   通过随机设置选项值来创建./.config文件。
- `make localmodconfig` 基于当前配置和加载的模块（lsmod）创建配置。禁用已加载的模块不需要的任何模块选项。
- `make localyesconfig` 与localmodconfig类似，只是它会将所有模块选项转换为内置（=y）。你可以同时通过LMC_KEEP保留模块。
- `make kvm_guest.config` 为kvm客户机内核支持启用其他选项。
- `make xen.config`   为xen dom0客户机内核支持启用其他选项。
- `make tinyconfig`   配置尽可能小的内核。

> [The Linux Kernel documentation](https://docs.kernel.org/index.html)
