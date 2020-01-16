<a href="https://mengduanxian.github.io/">梦断弦の小窝</a>

# Operating System Introduction

## What is an Operating System?

* Operating System is a ***software*** that <u>controls the execution of programs</u> and that <u>provides services</u> such as *resource allocation*, *scheduling*, *input/output control*, and *data management*. 
* The OS acts as an intermediary between a user of the computer and the computer hardware.
* OS goals: 
  * Execute user programs and make solving user problems easier.
  * Make the computer hardware in an efficient manner. (efficient manner - time and space efficiency, 大O表示的那个)

## Computer System Components

1. **Hardware** - provides basic computing resources(CPU, memory, I/O devices).
2. **Operating System** - controls and coordinates the use of the hardware among the various users. 
3. **Application programs** - define the ways in which the system resources are used to solve the computing problems of the users (compiler, database systems, video games, business programs).
4. **Users** - people, machines, other computers. 

## Abstract view of system components

<img src="img/abstractViewofOS.png" />



## Definitions

You can think of an Operating System as a:

* **resource allocator** - manages and allocates resources. 
* **control program** - controls the execution of user programs and operations of I/O devices. 
* **Kernel** - the one program running at all times (all else being application programs).

## Computer Startup

A *bootstrap program(引导程序)* is loaded at power-up or reboot.

* Typically stored in ROM or EPROM (Electrically Programmable Read-Only-Memory可擦可编程只读存储器), generally known as firmware(固件). 
* Initializes all aspects of the system. 
* Loads operating system kernel and starts execution. 

## Computer System Organization

Computer-system operation 计算机系统操作

* One or more CPUs, device controllers connect through a common bus providing access to shared memory. 

  (一个或多个CPU、设备控制器通过一条公共总线连接，以提供对共享内存的访问。)

<img src="img/typicalPCcomputersystem.png" />



## Interrupts

* We want the I/O devices and the CPU to be able to execute concurrently.
  * The CPU shouldn't have to wait for the much slower I/O device. 
* The I/O device signals an *interrupt* when it is ready. (I / O设备准备就绪时会发出“中断”信号。)
* When an interrupt occurs, the operating system must:
  * Transfer control to the appropriate interrupt handler.
  * Since there is more than one device, we use an interrupt vector (中断向量).

## Interrupts: Controllers vs. Handlers

* A device controller (hardware / firmware) is responsible for moving data between the <u>media</u> and its <u>local registers</u>. 
* An interrupt handler (software) is responsible for moving data between the <u>controller registers</u> and <u>memory</u> (so it can be accessed by the user program).
  * Since these are multiple types of interrupts, there is a handler for each type. 

## Processing an Interrupt

1. User program has control
2. I/O interrupt occurs
   * eg. disk controller signals data read operation completed. (磁盘控制器发出数据读取操作已完成的信号。)
3. User program no longer processed by the CPU
   * current position saved (Program Counter) and interrupt disabled. 
4. Control transferred to interrupt handler (控制权转移到中断处理程序)
   * CPU registers representing current state are saved. (保存代表当前状态的CPU寄存器。)
5. Data transferred from controller to memory or from memory to controller depending on whether input or output operation. 
6. CPU registers restored. (CPU寄存器恢复)
7. Control returned to user program. 
   * interrupts re-enabled & restore program counter. (中断重新启用并恢复程序计数器)

## I/O Structure

* The CPU and device controllers operate in parallel.