---
layout: post
title: '[OS] Solution Manual : System Structures ch02'
date: 2014-04-15 11:05
comments: true
tags: [OS]
---
2.1

The service and functions provided by an operating system can be divided into two main tags. Briefly describes the two tags and discuss how they differ. 

Ans:

**One class** of services provided by an operating system is to **enforce protection between different processes running concurrently in the system**. **Processes are allowed to access only those memory locations that are associated with their address spaces**. Also, processes are not allowed to corrupt files associated with other users. **A process is also not allowed to access devices directly without operating system intervention**.

**The second class** of services provided by an operating system is to **provide new functionality that is not supported directly by the underlying hardware**. **Virtual memory** and **file systems** are two such examples of new services provided by an operating system. 

2.2

Describe three general methods for passing parameters to the operating system.

Ans:

Register, Block, Stack

1. pass the parameters in registers
2. Parameters stored in a block,or table,in memory,and address of block passed as a parameter in a register
3. Parameters placed,or pushed, onto the stack by the program and popped off the stack by the operating system

2.3

Describe how you could obtain a statistical profile of the amount of time spent by a program executing different sections of its code. Discuss the importance of obtaining such statistical profile.

Ans:

One could **issue periodic timer interrupts** and **monitor what instructions or what sections of code are currently executing when the interrupts are delivered**. A statistical profile of which pieces of code were active should be **consistent with the time spent by the programin different sections of its code.**

Once statistical profile has been obtained, the programmer could**optimize those sections of code that are consuming more of the CPU resources.**

http://wiki.answers.com/Q/Describe_how_you_could_obtain_a_statistical_profile_of_the_amount_of_time_spent_by_a_program_executing_different_sections_of_its_code?#slide=7

2.4

What are the five major activities of an operating system with regard to file management?

Ans:

The creation and deletion of files

The creation and deletion of directories

The support of primitives for manipulating files and directories （open, close, read, write, reposition）

The mapping of files onto secondary storage

The backup of files on stable (nonvolatile) storage media

2.5

What are the advantages and disadvantages of using the same system-call interface for manipulating both files and devices?

Ans:

**Each device can be accessed as though it was a file in the filesystem**. Since most of the kernel deals with devices through this file interface,it is relatively easy to add a new device driver by implementing the hardware-specific code to support this abstract file interface. Therefore,t**his benefits the development of both user program code, which can be written to access devices and files in the same manner**, and device driver code, which can be written to support a well-defined API.

**The disadvantage with using the same interface** is that **it might be difficult to capture the functionality of certain devices within the context of the file access API**, **thereby either resulting in a loss of functionality or a loss of performance**. Some of this could be overcome by the use of ioctl operationthat provides a general purpose interface for processes to invokeoperations on devices.

http://quizlet.com/13315241/operating-systems-ch-2-flash-cards/

2.6

Would it be possible for the user to develop a new command intepreter using the system-call interface provided by the operating system

Ans:

Yes.

be able to develop a new command interpreter using the system-call interface provided by the operating system. **The command interpreter allows an user to create and manage processes and also determine ways by which they communicate (such as through pipes and files).** As all of this functionality could be accessed by an user-level program using the system calls, so it should be possible for the user to develop a new command-line interpreter.

2.7

What are the two models of interprocess communication? what are the strengths and weaknesses of the two approaches?

Ans:

One is **message-passing model** and the other is **shared-memory model**.

**Message-passing strengths and weaknesses**: **message can be exchanged between the processes either directly or indirectly through a common mailbox**. it is userful for exchanging smaller amounts of data and easier to implement for intercomputer communication. however,**its speed is slower than shared-memory model**.

**Shared-memory strengths and weaknesses**: it **allows maxmum speed and convenience of communication**. however,**in the areas of protection and synchronization between the processes some problems exist**.

2.8

Why is the separation of mechanism and policy desirable? 

Ans:

The separation of mechanism and policy is important to **provide flexibility to a system**. If the interface between mechanism and policy is well defined, **the change of policy may affect only a few parameters**. On the other hand, if interface between these two is vague or not well defined, it might involve much deeper change to the system.

Mechanism and policy must be separate to ensure that systems **are 
easy to modify**.

http://wiki.answers.com/Q/Why_is_the_separation_of_mechanism_and_policy_desirable?#slide=6

http://ce.sharif.edu/courses/86-87/2/ce424/resources/root/Assignment%20Answers/OS-HW2%20Answers.pdf

2.9

It is sometimes difficult to achieve a layered approach if two components of the operating system are dependent on each other. Identify a scenario in which it is unclear how to layer two system components that require tight coupling of their functionalities.

Ans:

The **virtual memory subsystem** and the **storage subsystem** are typically tightly coupled and require careful design in a layered system due to the following interactions. 

Many **systems allow files to be mapped into the virtual memory space of an executing process**. **On the other hand, the virtual memory subsystem typically uses the storage system to provide the backing store for pages that do not currently reside in memory.**

Also, updates to the file system are sometimes buffered in **physical memory** before it is **flushed to disk**, thereby requiring **careful coordination of the usage of memory between the virtual memory subsystem and the file system**.

https://www.google.com.tw/url?sa=t&rct=j&q=&esrc=s&source=web&cd=2&ved=0CC4QFjAB&url=http%3A%2F%2Fportal.unimap.edu.my%3A7778%2Fportal%2Fpage%2Fportal30%2FLecturer%2520Notes%2FKEJURUTERAAN_KOMPUTER%2FSemester%25202%2520Sidang%2520Akademik%252020102011%2FDKT%2520221%2520Operating%2520System%2520Principle%2FTutorials%2FAnswers%2FSolutions%25202.docx&ei=sTFNU532K5CtkgXimoCoCA&usg=AFQjCNECZ54D48gtLMQBxEcVF1Ot-b9PZQ

2.10

What are the main advantages of the microkernel approach to system design?

How do user programs and system services interact in a microkernel architecture?

What are the disadvantages of using the microkernel approach?

Ans:

Beneﬁts typically include the following (a) adding a new service does **not require modifying the kernel**, (b) it is **more secure** as **more operations are done in user mode than in kernel mode**, and (c) a **simpler** kernel design and functionality typically results in a **more reliable** operating system.

User programs and system services could interact through **message passing** or **shared memory** .

the disadvantages is : suffer from **performance decreases** due to **increased system function overhead** (context switching increased).

http://wiki.answers.com/Q/What_are_the_disadvantages_of_a_microkernel?r2as=1#slide=2

http://answers-by-me.blogspot.tw/2010/11/operating-system-concepts-8e-exercise_8677.html

http://codex.cs.yale.edu/avi/os-book/OS8/os8j/practice-exer-dir/2-web.pdf

2.11

What are the advantages of using loadable kernel modules?

Ans:

Each is **loadable as needed** within the kernel with **more flexible**

2.12

How are iOS and Android similar, How are they different?

Ans:

the main similarities are: Android and iOS are **both operating systems for mobile devices**. They are **both programmed in C and C++**.

the differences are: **Android is an open-source** OS and **iOS is a closed source** OS.

ios is based on Mac OS X kernel.

android is based on Linux kernel.

http://wiki.answers.com/Q/How_are_iOS_and_Android_similar_How_are_they_different?#slide=5

2.13

Explain why java programs running on android systems do not use the standard java api and virtual machine?

Ans:

android api, Dalvik VM

2.14

Ans:(none)