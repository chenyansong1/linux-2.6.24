# Linux 2.6.24 内核学习笔记

## 参考书目

![1527994958691.png](image/1527994958691.png)

![1530431527612.png](image/1530431527612.png)


## 内容简介

本书讨论了Linux内核的概念、结构和实现。

主要内容包括多任务、调度和进程管理，物理内存的管理以及内核与相关硬件的交互，用户空间的进程如何访问虚拟内存，如何编写设备驱动程序，模块机制以及虚拟文件系统，Ext文件系统属性和访问控制表的实现方式，内核中网络的实现，系统调用的实现方式，内核对时间相关功能的处理，页面回收和页交换的相关机制以及审计的实现等。

此外，本书借助内核源代码中最关键的部分进行讲解，帮助读者掌握重要的知识点，从而在运用中充分展现Linux系统的魅力。


## 《深入Linux内核架构》目录

* 第1章　简介和概述
* 第2章　进程管理和调度
* 第3章　内存管理
* 第4章　进程虚拟内存
* 第5章　锁与进程间通信
* 第6章　设备驱动程序
* 第7章　模块
* 第8章　虚拟文件系统
* 第9章　Ext文件系统族
* 第10章　无持久存储的文件系统
* 第11章　扩展属性和访问控制表
* 第12章　网络
* 第13章　系统调用
* 第14章　内核活动
* 第15章　时间管理
* 第16章　页缓存和块缓存
* 第17章　数据同步
* 第18章　页面回收和页交换
* 第19章　审计
* 附录A　体系结构相关知识
* 附录B　使用源代码
* 附录C　有关C语言的注记
* 附录D　系统启动
* 附录E　ELF二进制格式
* 附录F　内核开发过程
* 参考文献

## 《Linux内核设计与实现》目录

* 第1章　Linux内核简介
* 第2章　从内核出发
* 第3章　进程管理
* 第4章　进程调度
* 第5章　系统调用
* 第6章　内核数据结构
* 第7章　中断和中断处理
* 第8章　下半部和推后执行的工作
* 第9章　内核同步介绍
* 第10章　内核同步方法
* 第11章　定时器和时间管理
* 第12章　内存管理
* 第13章　虚拟文件系统
* 第14章　块I/O层
* 第15章　进程地址空间
* 第16章　页高速缓存和页回写
* 第17章　设备与模块
* 第18章　调试
* 第19章　可移植性
* 第20章　补丁、开发和社区
* 参考资料


## Kernel README

	Linux kernel release 2.6.xx <http://kernel.org/>

These are the release notes for Linux version 2.6.  Read them carefully,
as they tell you what this is all about, explain how to install the
kernel, and what to do if something goes wrong.

WHAT IS LINUX?

  Linux is a clone of the operating system Unix, written from scratch by
  Linus Torvalds with assistance from a loosely-knit team of hackers across
  the Net. It aims towards POSIX and Single UNIX Specification compliance.

  It has all the features you would expect in a modern fully-fledged Unix,
  including true multitasking, virtual memory, shared libraries, demand
  loading, shared copy-on-write executables, proper memory management,
  and multistack networking including IPv4 and IPv6.

  It is distributed under the GNU General Public License - see the
  accompanying COPYING file for more details.

ON WHAT HARDWARE DOES IT RUN?

  Although originally developed first for 32-bit x86-based PCs (386 or higher),
  today Linux also runs on (at least) the Compaq Alpha AXP, Sun SPARC and
  UltraSPARC, Motorola 68000, PowerPC, PowerPC64, ARM, Hitachi SuperH, Cell,
  IBM S/390, MIPS, HP PA-RISC, Intel IA-64, DEC VAX, AMD x86-64, AXIS CRIS,
  Xtensa, AVR32 and Renesas M32R architectures.

  Linux is easily portable to most general-purpose 32- or 64-bit architectures
  as long as they have a paged memory management unit (PMMU) and a port of the
  GNU C compiler (gcc) (part of The GNU Compiler Collection, GCC). Linux has
  also been ported to a number of architectures without a PMMU, although
  functionality is then obviously somewhat limited.
  Linux has also been ported to itself. You can now run the kernel as a
  userspace application - this is called UserMode Linux (UML).

DOCUMENTATION:

 - There is a lot of documentation available both in electronic form on
   the Internet and in books, both Linux-specific and pertaining to
   general UNIX questions.  I'd recommend looking into the documentation
   subdirectories on any Linux FTP site for the LDP (Linux Documentation
   Project) books.  This README is not meant to be documentation on the
   system: there are much better sources available.

 - There are various README files in the Documentation/ subdirectory:
   these typically contain kernel-specific installation notes for some
   drivers for example. See Documentation/00-INDEX for a list of what
   is contained in each file.  Please read the Changes file, as it
   contains information about the problems, which may result by upgrading
   your kernel.

 - The Documentation/DocBook/ subdirectory contains several guides for
   kernel developers and users.  These guides can be rendered in a
   number of formats:  PostScript (.ps), PDF, and HTML, among others.
   After installation, "make psdocs", "make pdfdocs", or "make htmldocs"
   will render the documentation in the requested format.

INSTALLING the kernel:

 - If you install the full sources, put the kernel tarball in a
   directory where you have permissions (eg. your home directory) and
   unpack it:

		gzip -cd linux-2.6.XX.tar.gz | tar xvf -

   or
		bzip2 -dc linux-2.6.XX.tar.bz2 | tar xvf -


   Replace "XX" with the version number of the latest kernel.

   Do NOT use the /usr/src/linux area! This area has a (usually
   incomplete) set of kernel headers that are used by the library header
   files.  They should match the library, and not get messed up by
   whatever the kernel-du-jour happens to be.

 - You can also upgrade between 2.6.xx releases by patching.  Patches are
   distributed in the traditional gzip and the newer bzip2 format.  To
   install by patching, get all the newer patch files, enter the
   top level directory of the kernel source (linux-2.6.xx) and execute:

		gzip -cd ../patch-2.6.xx.gz | patch -p1

   or
		bzip2 -dc ../patch-2.6.xx.bz2 | patch -p1

   (repeat xx for all versions bigger than the version of your current
   source tree, _in_order_) and you should be ok.  You may want to remove
   the backup files (xxx~ or xxx.orig), and make sure that there are no
   failed patches (xxx# or xxx.rej). If there are, either you or me has
   made a mistake.

   Unlike patches for the 2.6.x kernels, patches for the 2.6.x.y kernels
   (also known as the -stable kernels) are not incremental but instead apply
   directly to the base 2.6.x kernel.  Please read
   Documentation/applying-patches.txt for more information.

   Alternatively, the script patch-kernel can be used to automate this
   process.  It determines the current kernel version and applies any
   patches found.

		linux/scripts/patch-kernel linux

   The first argument in the command above is the location of the
   kernel source.  Patches are applied from the current directory, but
   an alternative directory can be specified as the second argument.

 - If you are upgrading between releases using the stable series patches
   (for example, patch-2.6.xx.y), note that these "dot-releases" are
   not incremental and must be applied to the 2.6.xx base tree. For
   example, if your base kernel is 2.6.12 and you want to apply the
   2.6.12.3 patch, you do not and indeed must not first apply the
   2.6.12.1 and 2.6.12.2 patches. Similarly, if you are running kernel
   version 2.6.12.2 and want to jump to 2.6.12.3, you must first
   reverse the 2.6.12.2 patch (that is, patch -R) _before_ applying
   the 2.6.12.3 patch.
   You can read more on this in Documentation/applying-patches.txt

 - Make sure you have no stale .o files and dependencies lying around:

		cd linux
		make mrproper

   You should now have the sources correctly installed.

SOFTWARE REQUIREMENTS

   Compiling and running the 2.6.xx kernels requires up-to-date
   versions of various software packages.  Consult
   Documentation/Changes for the minimum version numbers required
   and how to get updates for these packages.  Beware that using
   excessively old versions of these packages can cause indirect
   errors that are very difficult to track down, so don't assume that
   you can just update packages when obvious problems arise during
   build or operation.

BUILD directory for the kernel:

   When compiling the kernel all output files will per default be
   stored together with the kernel source code.
   Using the option "make O=output/dir" allow you to specify an alternate
   place for the output files (including .config).
   Example:
     kernel source code:	/usr/src/linux-2.6.N
     build directory:		/home/name/build/kernel

   To configure and build the kernel use:
   cd /usr/src/linux-2.6.N
   make O=/home/name/build/kernel menuconfig
   make O=/home/name/build/kernel
   sudo make O=/home/name/build/kernel modules_install install

   Please note: If the 'O=output/dir' option is used then it must be
   used for all invocations of make.

CONFIGURING the kernel:

   Do not skip this step even if you are only upgrading one minor
   version.  New configuration options are added in each release, and
   odd problems will turn up if the configuration files are not set up
   as expected.  If you want to carry your existing configuration to a
   new version with minimal work, use "make oldconfig", which will
   only ask you for the answers to new questions.

 - Alternate configuration commands are:
	"make config"      Plain text interface.
	"make menuconfig"  Text based color menus, radiolists & dialogs.
	"make xconfig"     X windows (Qt) based configuration tool.
	"make gconfig"     X windows (Gtk) based configuration tool.
	"make oldconfig"   Default all questions based on the contents of
			   your existing ./.config file and asking about
			   new config symbols.
	"make silentoldconfig"
			   Like above, but avoids cluttering the screen
			   with questions already answered.
	"make defconfig"   Create a ./.config file by using the default
			   symbol values from arch/$ARCH/defconfig.
	"make allyesconfig"
			   Create a ./.config file by setting symbol
			   values to 'y' as much as possible.
	"make allmodconfig"
			   Create a ./.config file by setting symbol
			   values to 'm' as much as possible.
	"make allnoconfig" Create a ./.config file by setting symbol
			   values to 'n' as much as possible.
	"make randconfig"  Create a ./.config file by setting symbol
			   values to random values.

   The allyesconfig/allmodconfig/allnoconfig/randconfig variants can
   also use the environment variable KCONFIG_ALLCONFIG to specify a
   filename that contains config options that the user requires to be
   set to a specific value.  If KCONFIG_ALLCONFIG=filename is not used,
   "make *config" checks for a file named "all{yes/mod/no/random}.config"
   for symbol values that are to be forced.  If this file is not found,
   it checks for a file named "all.config" to contain forced values.

	NOTES on "make config":
	- having unnecessary drivers will make the kernel bigger, and can
	  under some circumstances lead to problems: probing for a
	  nonexistent controller card may confuse your other controllers
	- compiling the kernel with "Processor type" set higher than 386
	  will result in a kernel that does NOT work on a 386.  The
	  kernel will detect this on bootup, and give up.
	- A kernel with math-emulation compiled in will still use the
	  coprocessor if one is present: the math emulation will just
	  never get used in that case.  The kernel will be slightly larger,
	  but will work on different machines regardless of whether they
	  have a math coprocessor or not.
	- the "kernel hacking" configuration details usually result in a
	  bigger or slower kernel (or both), and can even make the kernel
	  less stable by configuring some routines to actively try to
	  break bad code to find kernel problems (kmalloc()).  Thus you
	  should probably answer 'n' to the questions for
          "development", "experimental", or "debugging" features.

COMPILING the kernel:

 - Make sure you have at least gcc 3.2 available.
   For more information, refer to Documentation/Changes.

   Please note that you can still run a.out user programs with this kernel.

 - Do a "make" to create a compressed kernel image. It is also
   possible to do "make install" if you have lilo installed to suit the
   kernel makefiles, but you may want to check your particular lilo setup first.

   To do the actual install you have to be root, but none of the normal
   build should require that. Don't take the name of root in vain.

 - If you configured any of the parts of the kernel as `modules', you
   will also have to do "make modules_install".

 - Keep a backup kernel handy in case something goes wrong.  This is
   especially true for the development releases, since each new release
   contains new code which has not been debugged.  Make sure you keep a
   backup of the modules corresponding to that kernel, as well.  If you
   are installing a new kernel with the same version number as your
   working kernel, make a backup of your modules directory before you
   do a "make modules_install".
   Alternatively, before compiling, use the kernel config option
   "LOCALVERSION" to append a unique suffix to the regular kernel version.
   LOCALVERSION can be set in the "General Setup" menu.

 - In order to boot your new kernel, you'll need to copy the kernel
   image (e.g. .../linux/arch/i386/boot/bzImage after compilation)
   to the place where your regular bootable kernel is found.

 - Booting a kernel directly from a floppy without the assistance of a
   bootloader such as LILO, is no longer supported.

   If you boot Linux from the hard drive, chances are you use LILO which
   uses the kernel image as specified in the file /etc/lilo.conf.  The
   kernel image file is usually /vmlinuz, /boot/vmlinuz, /bzImage or
   /boot/bzImage.  To use the new kernel, save a copy of the old image
   and copy the new image over the old one.  Then, you MUST RERUN LILO
   to update the loading map!! If you don't, you won't be able to boot
   the new kernel image.

   Reinstalling LILO is usually a matter of running /sbin/lilo.
   You may wish to edit /etc/lilo.conf to specify an entry for your
   old kernel image (say, /vmlinux.old) in case the new one does not
   work.  See the LILO docs for more information.

   After reinstalling LILO, you should be all set.  Shutdown the system,
   reboot, and enjoy!

   If you ever need to change the default root device, video mode,
   ramdisk size, etc.  in the kernel image, use the 'rdev' program (or
   alternatively the LILO boot options when appropriate).  No need to
   recompile the kernel to change these parameters.

 - Reboot with the new kernel and enjoy.

IF SOMETHING GOES WRONG:

 - If you have problems that seem to be due to kernel bugs, please check
   the file MAINTAINERS to see if there is a particular person associated
   with the part of the kernel that you are having trouble with. If there
   isn't anyone listed there, then the second best thing is to mail
   them to me (torvalds@linux-foundation.org), and possibly to any other
   relevant mailing-list or to the newsgroup.

 - In all bug-reports, *please* tell what kernel you are talking about,
   how to duplicate the problem, and what your setup is (use your common
   sense).  If the problem is new, tell me so, and if the problem is
   old, please try to tell me when you first noticed it.

 - If the bug results in a message like

	unable to handle kernel paging request at address C0000010
	Oops: 0002
	EIP:   0010:XXXXXXXX
	eax: xxxxxxxx   ebx: xxxxxxxx   ecx: xxxxxxxx   edx: xxxxxxxx
	esi: xxxxxxxx   edi: xxxxxxxx   ebp: xxxxxxxx
	ds: xxxx  es: xxxx  fs: xxxx  gs: xxxx
	Pid: xx, process nr: xx
	xx xx xx xx xx xx xx xx xx xx

   or similar kernel debugging information on your screen or in your
   system log, please duplicate it *exactly*.  The dump may look
   incomprehensible to you, but it does contain information that may
   help debugging the problem.  The text above the dump is also
   important: it tells something about why the kernel dumped code (in
   the above example it's due to a bad kernel pointer). More information
   on making sense of the dump is in Documentation/oops-tracing.txt

 - If you compiled the kernel with CONFIG_KALLSYMS you can send the dump
   as is, otherwise you will have to use the "ksymoops" program to make
   sense of the dump (but compiling with CONFIG_KALLSYMS is usually preferred).
   This utility can be downloaded from
   ftp://ftp.<country>.kernel.org/pub/linux/utils/kernel/ksymoops/ .
   Alternately you can do the dump lookup by hand:

 - In debugging dumps like the above, it helps enormously if you can
   look up what the EIP value means.  The hex value as such doesn't help
   me or anybody else very much: it will depend on your particular
   kernel setup.  What you should do is take the hex value from the EIP
   line (ignore the "0010:"), and look it up in the kernel namelist to
   see which kernel function contains the offending address.

   To find out the kernel function name, you'll need to find the system
   binary associated with the kernel that exhibited the symptom.  This is
   the file 'linux/vmlinux'.  To extract the namelist and match it against
   the EIP from the kernel crash, do:

		nm vmlinux | sort | less

   This will give you a list of kernel addresses sorted in ascending
   order, from which it is simple to find the function that contains the
   offending address.  Note that the address given by the kernel
   debugging messages will not necessarily match exactly with the
   function addresses (in fact, that is very unlikely), so you can't
   just 'grep' the list: the list will, however, give you the starting
   point of each kernel function, so by looking for the function that
   has a starting address lower than the one you are searching for but
   is followed by a function with a higher address you will find the one
   you want.  In fact, it may be a good idea to include a bit of
   "context" in your problem report, giving a few lines around the
   interesting one.

   If you for some reason cannot do the above (you have a pre-compiled
   kernel image or similar), telling me as much about your setup as
   possible will help.  Please read the REPORTING-BUGS document for details.

 - Alternately, you can use gdb on a running kernel. (read-only; i.e. you
   cannot change values or set break points.) To do this, first compile the
   kernel with -g; edit arch/i386/Makefile appropriately, then do a "make
   clean". You'll also need to enable CONFIG_PROC_FS (via "make config").

   After you've rebooted with the new kernel, do "gdb vmlinux /proc/kcore".
   You can now use all the usual gdb commands. The command to look up the
   point where your system crashed is "l *0xXXXXXXXX". (Replace the XXXes
   with the EIP value.)

   gdb'ing a non-running kernel currently fails because gdb (wrongly)
   disregards the starting offset for which the kernel is compiled.
