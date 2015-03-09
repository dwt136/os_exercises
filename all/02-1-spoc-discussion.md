#lec 3 SPOC Discussion

## 第三讲 启动、中断、异常和系统调用-思考题

## 3.1 BIOS
 1. 比较UEFI和BIOS的区别。
 1. 描述PXE的大致启动流程。

## 3.2 系统启动流程
 1. 了解NTLDR的启动流程。
 1. 了解GRUB的启动流程。
 1. 比较NTLDR和GRUB的功能有差异。
 1. 了解u-boot的功能。

## 3.3 中断、异常和系统调用比较
 1. 举例说明Linux中有哪些中断，哪些异常？
 1. Linux的系统调用有哪些？大致的功能分类有哪些？  (w2l1)

```
Linux全部系统调用有250个左右，大致分类为进程控制、文件操作、系统控制、内存管理、网络管理和用户管理等。
```
 
 1. 以ucore lab8的answer为例，uCore的系统调用有哪些？大致的功能分类有哪些？(w2l1)
 
```
uCore系统调用有二十几个，大致分类为文件操作、进程管理和内存管理等。
```
 
## 3.4 linux系统调用分析
 1. 通过分析[lab1_ex0](https://github.com/chyyuu/ucore_lab/blob/master/related_info/lab1/lab1-ex0.md)了解Linux应用的系统调用编写和含义。(w2l1)
 

```
1. 编译lab1_ex0，可用file查看其文件类型，为ELF可执行文件。执行该输出文件，在屏幕上打出hello world。
2. 可用objdump查看输出文件的汇编代码。
3. 可用nm查看输出程序的符号表。
分析其代码，可以看出程序进行系统调用的过程是调用函数，并传入参数，由操作系统进行相应的操作。
```
 
 1. 通过调试[lab1_ex1](https://github.com/chyyuu/ucore_lab/blob/master/related_info/lab1/lab1-ex1.md)了解Linux应用的系统调用执行过程。(w2l1)
 

```
strace可用于跟踪进程执行时的系统调用和所接收的信号。
在linux系统调用中，程序调用POSIX API，通过中断进入内核态，内核态中的中断处理函数根据系统调用号调用相应的系统函数，并在处理结束后返回用户态，同时返回到API，然后返回到用户程序。
```
 
## 3.5 ucore系统调用分析
 1. ucore的系统调用中参数传递代码分析。
 1. ucore的系统调用中返回结果的传递代码分析。
 1. 以ucore lab8的answer为例，分析ucore 应用的系统调用编写和含义。
 1. 以ucore lab8的answer为例，尝试修改并运行ucore OS kernel代码，使其具有类似Linux应用工具`strace`的功能，即能够显示出应用程序发出的系统调用，从而可以分析ucore应用的系统调用执行过程。
 
## 3.6 请分析函数调用和系统调用的区别
 1. 请从代码编写和执行过程来说明。
   1. 说明`int`、`iret`、`call`和`ret`的指令准确功能
 
