# 寄存器
15
- rax rcx rdx rbx
- rsp rbp
- rsi rdi
- r8 - r14

width: 64bit (int64_t)

rsp: stack pointer

# 条件码
- zf, sf, of
- width: 1bit


# 指令

## movq
- 子指令
  - irmovq
  - rrmovq
  - mrmovq
  - rmmovq

*i立即数 r寄存器 m内存*

- 寻址方式
  - 简单的基址和偏移量

- misc
  - 不允许m2m， i2m

## 整数操作指令 OPq
- 子指令
  - addq
  - subq
  - andq
  - xorq
- 对象
  - 仅仅寄存器数据
- misc
  - 设置三个条件码，zf零，sf符号，of溢出

## 跳转指令

- 子指令
  - jmp
  - jle
  - jl
  - je
  - jne
  - jge
  - jg
- 绝对地址寻址


## 条件传送指令

- 子指令
  - cmovl
  - cmovle
  - cmove
  - cmovne
  - cmovg
  - cmovge


## 调用

- call返回地址入栈，跳到目的地址
- ret返回

## 栈

- pushq
- popq

## misc

- halt停止处理器执行，并将状态码设置为hlt

![instructions encpding](instructions.png)

![reg encode](regencode.png)

![state code](statcode.png)

# 其余要求

1. 能够输出寄存器，储存器的值 
   
   - 类似gdb调试的窗口，同时增加list指令 done.
  
listq $imm // list word at address $imm
listc %reg

or

list $imm(%reg), 0xf
list 0, 0xf, %reg [accepted]

list D(%reg), %reg
- list 0xf, %reg show %reg
- list D(%reg), 0xf show [reg + d]

1. 正确性检验
   - 增加输出指定信息的函数
   - 脚本检验


# todo list
1. 重构执行指令函数 done.
   - 所有类型的指令函数参数统一,均为所需参数的指针(同时都返回void)
   - 将上述函数的指针存到一个数组里
   - exec-single-instruction中通过调用函数将所有参数进行解码,传参

2. 增加命令行参数
   1. 调试选项,实时打印寄存器和存储,实现反汇编功能 done.
   2. 输出文件,将寄存器和内存输出到指定文件done.


3. python脚本测试模拟器正确性