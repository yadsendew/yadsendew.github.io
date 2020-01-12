---
layout: post
title: Operating Systems Notes
date: 2019-12-30 21:21 +0000
categories: [Learning]
tags: [Operating Systems]
ordered: true
---

## Slide 1

- **User processes** process the users’ jobs
- **System processes** provide services of the operating system
- The OS core (kernel) contains all components of the operating system, which are **not** implemented as system processes

### Operating Systems are Part of the System Software

    System software controls the operation of a computer, assists users and their applications in making use of the hardware and controls the use and allocation of the available hardware resources

## Slide 2
Learning objectives:  
- Slide 1
  - Operating Systems are Part of the System Software
- Slide 2
  - Singletasking & Multitasking
  - Single-user & multi-user
  - Memory Address Length
  - Real-Time Operating Systems
    - Hard and Soft Real-Time Operating Systems
    - Architectures of Real-Time Operating Systems
  - Distributed Operating Systems
    - Distributed Operating Systems – Situation Today
  - Kernel Architectures
    - Monolithic Kernels (Monolithic = nguyên khối)
    - Microkernels
### Singletasking & Multitasking
_Singletasking_: At any given moment, only a single program is executed. Multiple started programs are executed one after the other.  
_Multitasking_: with multitasking, multiple processes are executed at the same time (concurrently). The processes are activated alternately at short intervals. For this reason, the execution appears simultaneous. Drawback: Switching from one process to another one causes overhead.  

Why multitasking?
* Processes often need to wait for external events. 
  * External events may be user inputs, input/output operations of peripheral devices, or simply waiting for a message from another program With multi-tasking, processes, which wait for incoming E-mails, successful database operations, data written to the HDD or something similar can be placed in the background. => This way, other processes can be executed sooner
* The program switching, which is required to implement the quasi-parallel execution, causes overhead
  * The overhead is rather small compared with the speedup
### Single-user & multi-user
_Single-User_  the computer can only be used by single user at any point in time

_Multiple users_ can work simultaneously with the computer.
* Users share the system resources (as fair as possible) 
* Users must be identiﬁed (via passwords) 
* Access to data/processes of other users must be prevented

_Half multi-user operating systems_ Diﬀerent users can work with the system only one after the other, but the data and processes of the diﬀerent users are protected from each other.

### Memory Address Length
    8/16/32/64 bit is the number of memory units, an operating system can address.
    32 bit OS can address 2^32 memory units.
### Real-Time Operating Systems
_Real-Time OS_ are multitasking operating systems with additional real-time functions for the compliance of time conditions (chức năng thời gian thực cho việc tuân thủ các điều kiện thời gian).  
Essential criteria of real-time operating systems:
* Response time 
* Meet deadlines

Diﬀerent priorities are taken into account so that important processes are executed within certain time limits.
2 types of real-time operating systems exist:
* Hard real-time operating systems
* Soft real-time operating systems

Modern desktop OS can guarantee soft real-time behavior for processes with high priority
* Because of the unpredictable time behavior due to swapping, hardware interrupts, etc. hard real-time behavior cannot be guaranteed

#### Hard and Soft Real-Time Operating Systems
Hard real-time operating systems
* Deadlines must be strictly met 
* Delays cannot be accepted under any circumstances 
* Delays lead to disastrous consequences and high cost 
* Results are useless if they are achieved too late 
* Application examples: Welding robot, reactor control, Anti-lock braking system (ABS), aircraft ﬂight control, monitoring systems of an intensive care unit.  

Soft real-time operating systems
* Certain tolerances are allowed 
* Delays cause acceptable costs 
* Typical applications: Telephone system, parking ticket vending machine, ticket machine, multimedia applications such as audio/video on demand

#### Architectures of Real-Time Operating Systems
![](/assets/img/2020-01-11-12-38-42.png)

Thin kernel

* The operating system kernel itself runs as a process with lowest priority 
* The real-time kernel does the scheduling 
* Real-time processes have the highest priority =⇒ minimum reaction time (latency)

Nano kernel

* In addition to the real-time kernel, any number of kernels of other operating systems may be executed

Pico kernel, Femto kernel, Atto kernel

* Marketing buzz-words of vendors of real-time operating systems to emphasize the smallness of their real-time kernel

### Distributed Operating Systems
Distributed system  
Controls processes on multiple computers of a cluster  
The individual computers remain transparently hidden from the users and their applications
* The system appears as a single large computer
  *  Single System Image principle

![](/assets/img/2020-01-11-12-51-18.png)
#### Distributed Operating Systems – Situation Today
The concept did not gain acceptance:
* Distributed operating systems never left research projects state 
* Established operating systems have never been replaced

For developing cluster applications, libraries exist, which provide hardware-independent message passing:
* Message passing communication is based on message exchange 
* Popular message passing systems:
  * Message Passing Interface (MPI) ⇒ standard solution 
  * Parallel Virtual Machine (PVM) ⇒ dead  

![](/assets/img/2020-01-11-12-54-44.png)
### Kernel Architectures
Kernel = essential functions of OS + interface to the hardware  
Diﬀerent kernel architectures exist
* They diﬀer in which functions are included inside in the kernel and which functions are outside the kernel as services (servers)

Functions in the kernel, have full hardware access (kernel mode)  
Functions outside the kernel can only access their virtual memory (user mode) => Slide 5
![](/assets/img/2020-01-12-21-27-54.png)
#### Monolithic Kernels (Monolithic = nguyên khối)
Contain functions for:
* memory management 
* process management 
* interprocess communication 
* hardware management (drivers) 
* ﬁle systems
  
**Advantages:**

* Fewer context switching as with microkernels =⇒ better performance  
* Grown stability: microkernels are usually not more stable compared with monolithic kernels

**Drawbacks:**
* Crashed kernel components can not be restarted separately and may cause the entire system to crash 
* Kernel extensions cause a high development eﬀort, because for each compilation of the extension, the complete kernel need to be recompiled  

It is possible to outsource drivers of the Linux kernel into modules. However, the modules are executed in kernel mode and not in the user mode. Therefore, the Linux kernel is a monolithic kernel.
#### Microkernels