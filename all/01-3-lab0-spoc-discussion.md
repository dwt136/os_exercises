# lab0 SPOC思考题

## 个人思考题

---

能否读懂ucore中的AT&T格式的X86-32汇编语言？请列出你不理解的汇编语言。
- [x]  

>  能

虽然学过计算机原理和x86汇编（根据THU-CS的课程设置），但对ucore中涉及的哪些硬件设计或功能细节不够了解？
- [x]  

> 暂无


哪些困难（请分优先级）会阻碍你自主完成lab实验？
- [x]  

> 1. 本课程或其他课程在Deadline时任务过重
> 2. 缺少完成实验需要的资源

如何把一个在gdb中或执行过程中出现的物理/线性地址与你写的代码源码位置对应起来？
- [x]  

> 在编译时加入参数，如-g。然后在gdb中即可显示断点的行号，同时可以通过gdb的list命令等方法来确定对应位置。


了解函数调用栈对lab实验有何帮助？
- [x]  

> 在实验代码中插入汇编代码时需要了解调用栈的结构。


你希望从lab中学到什么知识？
- [x]  

> 学习ucore的实现细节，了解一般操作系统的结构和实现方法，增强阅读和编写代码的能力。
 

---

## 小组讨论题

---

搭建好实验环境，请描述碰到的困难和解决的过程。
- [x]  

> 使用课程提供的虚拟机文件，搭建完成。

熟悉基本的git命令行操作命令，从github上
的 http://www.github.com/chyyuu/ucore_lab 下载
ucore lab实验
- [x]  

> git clone http://www.github.com/chyyuu/ucore_lab

尝试用qemu+gdb（or ECLIPSE-CDT）调试lab1
- [x]   

> make clean \
> lab1：make \
> debug命令行：make debug

对于如下的代码段，请说明”：“后面的数字是什么含义
```
 /* Gate descriptors for interrupts and traps */
 struct gatedesc {
    unsigned gd_off_15_0 : 16;        // low 16 bits of offset in segment
    unsigned gd_ss : 16;            // segment selector
    unsigned gd_args : 5;            // # args, 0 for interrupt/trap gates
    unsigned gd_rsv1 : 3;            // reserved(should be zero I guess)
    unsigned gd_type : 4;            // type(STS_{TG,IG32,TG32})
    unsigned gd_s : 1;                // must be 0 (system)
    unsigned gd_dpl : 2;            // descriptor(meaning new) privilege level
    unsigned gd_p : 1;                // Present
    unsigned gd_off_31_16 : 16;        // high bits of offset in segment
 };
 ```

- [x]  

> 该字段所占的的长度(bit).

对于如下的代码段，
```
#define SETGATE(gate, istrap, sel, off, dpl) {            \
    (gate).gd_off_15_0 = (uint32_t)(off) & 0xffff;        \
    (gate).gd_ss = (sel);                                \
    (gate).gd_args = 0;                                    \
    (gate).gd_rsv1 = 0;                                    \
    (gate).gd_type = (istrap) ? STS_TG32 : STS_IG32;    \
    (gate).gd_s = 0;                                    \
    (gate).gd_dpl = (dpl);                                \
    (gate).gd_p = 1;                                    \
    (gate).gd_off_31_16 = (uint32_t)(off) >> 16;        \
}
```
如果在其他代码段中有如下语句，
```
unsigned intr;
intr=8;
SETGATE(intr, 0,1,2,3);
```
请问执行上述指令后， intr的值是多少？

- [x]  65538

> https://github.com/chyyuu/ucore_lab/blob/master/related_info/lab0/lab0_ex3.c

请分析 [list.h](https://github.com/chyyuu/ucore_lab/blob/master/labcodes/lab2/libs/list.h)内容中大致的含义，并能include这个文件，利用其结构和功能编写一个数据结构链表操作的小C程序
- [x]  
```
// ---------- test_list.c ----------
#include "list.h"
#include 

int main() {
  int i;
  struct list_entry e[4];
  for (i = 0; i < 4; i ++) {
    list_init(e + i);
  }
  list_add_after(&e[0], &e[1]);
  list_add_after(&e[1], &e[2]);
  list_del_init(&e[0]);
  printf("%d %d\n", list_next(&e[2]) == &e[1], list_prev(&e[1]) == &e[2]);
  printf("%d %d\n", list_empty(&e[0]), list_empty(&e[1]));
  return 0;
}
// Result:
// 1 1
// 1 0
```

---

## 开放思考题

---

是否愿意挑战大实验（大实验内容来源于你的想法或老师列好的题目，需要与老师协商确定，需完成基本lab，但可不参加闭卷考试），如果有，可直接给老师email或课后面谈。
- [x]  

> 否

---
