# SUSTech CS302: Operating System Lec1 - Lec3

[TOC]

# 1. Intro

### How a Modern Computer <font color="red">Works</font>?

- a single, shared <font color="red">memory</font> for programs and data
- a single <font color="red">bus</font> for memory access
- an <font color="red">arithmetic</font>(same means with “compute”) <font color="red">unit</font>
- a <font color="red">programe control unit</font>

### <font color="red">**Structure**</font> of a Computer System

Computer system can be divided into four components

- HardWare
- Operating System
- Application programs
- Users

<p align="center">
  <img src="picture/1-1.png" alt="structure" width=200 height=auto>
</p>


### Kernel

- A software included in OS.
- manages all the physical devices
- exposes some functions such as <font color="red">system calls</font> for others.

### OS

- A **Resource Manager.**
- A **Control Program**

### **What Does an Operating System <font color="red">Do</font>?**

- **Virtualization:** CPU and Memory
- **Concurrency:** multi thread
- **Persistence:** crash-resilience

## Concepts:

- **Process:** a program in execution.

# 2.  OS Basics

## 2.1: Dual-Mode Operations

Dual-mode (two modes) →<font color="red"> **user mode**</font> & <font color="red">**kernel mode**</font>

### 2.1.1: 3 types of <font color="red">Mode Transitions</font>

- System Call
- Interrupt
- Trap or Exception



#### System Calls

##### Types of System Calls <font color="red">(Mark)</font>:

<p align="center">
  <img src="picture/2-1.png" width=400 height=auto>
</p>

#### Exception (<font color="red">synchronous</font>) and Interrupt (<font color='red'>asynchronous</font>)

理解：

异常（Exception）同步于app运行发生。异常是执行某个<font color='red'>指令中</font>触发的。异常产生后，CPU会立即停止当前的工作，转去执行异常处理程序。

中断（Interrupt）是执行完某个<font color='red'>指令后</font>触发的。CPU会在完成当前的指令后切换到中断处理程序。



## 2.2 Kernel Structure

### 2.2.1 Monolithic Kernel

- Holds ==<font color="red">all privileges</font>== to access I/O devices, memory, hardware interrupts and the CPU stack.
- Contains many components.
- Basis of ==Linux, Unix, Ms-DOS== <font color="red">(Mark)</font>

### 2.2.2 Micro Kernel

- Outsource some function to <font color="red">user processes</font>.
- These user-level servers are trusted by kernel.



### 2.2.3 Hybrid Kernel & ExoKernel

<p align='center'>
  <img src="picture/2-2.png"style="width:60%;"/>
  <img src='picture/2-3.png'style="width:60%;"/>
</p>

### 2.2.4 OS Design Principles <font color='red'>(Mark)</font>

- **User goals**: operating system should be convenient to use, easy to learn, reliable, safe, and fast

- **System goals**: operating system should be easy to design, implement, and maintain, as well as flexible, reliable, error-free, and efficient25

- **OS separates policies and mechanisms**

  - Policy: which software could access which resource at what time
    - E.g., if two processes access the same device at the same time, which one goes first
    - E.g., if a process hopes to read from keyboard

  - Mechanism: How is the policy enforced

    - E.g., request queues for devices, running queues for CPUs

    - E.g., access control list for files, devices, etc.

  - The separation of policy from mechanism is a very important principle, it allows maximum flexibility if policy decisions are to be changed later26

## Operating System Services

### Operating System Services

- User Interface (UI)
- Program execution
- I/O operations
- File-system manipulation
- Communications
- Error detection
- Resource allocation
- Accounting
- Protection and security

# 3. Processes

- PID: process's unique ID number



### Process Life Cycle

<p float="left">
  <img src="picture/3-1.png" style='width:50%;'/>
</p>

**Notice:** A process ==<font color='red'>can not</font>== change directly from <font color='red'>running</font> to <font color='red'>ready</font>.



### System Call: Parameter Passing <font color='red'>(Mark)</font>

- Registers

- Blocks: stores in a <font color='red'>block</font>, and ==<font color='red'>address</font>== is passed by <font color='red'>registers</font>.

- Stack: parameters <font color='red'>pushed to stack</font> by ==program==, and <font color='red'>poped out</font> by ==operating system==

  

### 3 ways of process switch <font color='red'>(Mark)</font>

- Syscall

- Exception

- Interrupt

  

### Syscalls about Processes

**Note: ** One Process can **<font color='red'>only be</font>** created by ==<font color='red'>another process</font>==

#### 1. fork()

- In ==parent process==, it returns subprocess's <font color='red'>**PID**</font>;

  While In ==subprocess== created by fork() , it returns <font color='red'>**0**</font>.

- copy on write: subprocess <font color='red'>**shares the same memory**</font> with its parent process **unless** ==subprocess's memory== is ==**modified**==.

#### 2. exec()

**Note: **Exec() will **clear** origin process.

For example, process A do exec() to execute process B, then the rest of process A won't execute continually.

#### 3. wait() & waitpid

- Codes after wait() will execute after subprocess **terminated**.
- waitpid() do same thing with wait(). It waiting for a <font color='red'>specific pid</font>.

#### 4. exit()

- <font color='red'>**Zombie Processes:**</font> after exit(), process will not been recycled immediately until its parent <font color='red'>**reap**</font> it.

- After a process exit, a signal(SIGCHILD) will be broadcast.

- if its parent receive the signal, it will "<font color='red'>**reap**</font>" signal sender(sub-process, the "zombie").

  

<font color='red'>**Mark:**</font> exit() system call turns a process into a zombie when...

- The process calls exit().
- The process returns from main().
- The process terminates abnormally.
  - The kernel knows that the process is terminated abnormally. Hence, the kernel invokes exit() for it.

### PCB(Process Control Block)

- **PCB**: Information associated with each process.

  

### **Threads** and **Process** :

Process can have multiple threads. Threads in a process shared **codes**, **heap** and **files**, but have their own **stacks** and **registers**.

#### Thread Implementation

- User-level thread
  - Thread management (e.g., creating, scheduling, termination) done by user-level threads library
  - OS does not know aboutuser-level thread

- Kernel-level thread
  - Threat management done by kernel.
  - OS is aware of each kernel-level thread.

#### Thread Models.

<p align='center'>
  <img src='picture/3-2.png' style='width:50%;'/>
</p>

<p align='center'>
  <img src='picture/3-3.png'style='width:50%;'/>
</p>
















