---
layout: post
title: '[OS] Solution Manual : Process Concept ch03'
date: 2014-04-14 15:18
comments: true
tags: [OS]
---
3.1

Describe the differences among short term, medium term and long term sheduling?

Ans:

Short-term scheduler is invoked very frequently (milliseconds) ⇒ (must be fast)"

Long-term scheduler is invoked very infrequently (seconds, minutes) ⇒ (may be slow)"

3.2

Describe the actions taken by a kernel to switch between processes?

Ans:

the system must save the state of the old process and load the saved state for the new process via a context switch.

3.3

Ans:(none)

3.4

Explain the role of the init process on unix and linux system in regard to process termination?

Ans:

init is the parent of all processes. Its primary role is to create processes from a script stored in  the file /etc/inittab.

init is the first process started during booting of the computer system

3.5

Including the initial parent process, how many process are created by the program shown in Figure 3.31?

    #include <stdio.h>
    #include <unistd.h>

    int main() {
    	int i;
      
      for ( i = 0 ; i < 4 ; i++ ) {
          fork();
      }
      
      return 0;
    }


Ans:

1+4+3+2+1 = 11

3.6

Ans:(none)

3.7

Using the program in Figure 3.29, identify the values of pid at lines A, B, C and D. (Assume that the actual pids of the parent and child are 2600 and 2603, respectively.)

    #include <sys/types.h> 
    #include <stdio.h> 
    #include <unistd.h> 
     
    int main () 
    {
        /* fork a child process */ 
        pid = fork(); 
        if ( pid < 0 ) { /*error occurred 
            fprintf(stderr, “Fork Failed”); 
            return 1; 
        } 
        else if (pid ==0) { /* child process */ 
            pid1 = getpid(); 
            printf(“child: pid = %d” ,pid); /* A */ 
            printf(“child: pid1 = %d” ,pid1); /* B */ 
        } 
        else { /* parent process */ 
            pid1 = getpid(); 
            printf(“parent: pid = %d” ,pid); /* C */ 
            printf(“parent: pid1 = %d” ,pid1); /* D */ 
            wait(NULL); 
        } 
        return 0; 
    } 

Ans:

A: 0, B: 2603, C: 2603, D: 2600

http://hscc.cs.nthu.edu.tw/~sheujp/homework/os09/HW3_ref.pdf

3.8

Give an example of a situation in which ordinary pipes are more suitable than named pipes and an example of a situation in which named pipes are more suitable than ordinary pipes?

Ans:

ordinary pipes:

ordinary pipes require parent-child relationship between communicating processes.

ordinary pipes are unidirectional (producer-consumer style).

named pipes:

No parent-child relationship is necessary between the communicating processes.

named pipes is bidirectional.

3.9

Consider the RPC mechanism. Describe the undesirable circumstances that could arise from not enforcing either the "at most once" or "exactly once" semantics. Describe possible uses for a mechanism that had neither of these guarantees.

Ans:

If an RPC mechanism could not support either the "at most once" or "at least once" semantics, then the **RPC server cannot guarantee that a remote procedure will not be invoked multiple occurrences**. Consider if a remote procedure were **withdrawing money** from a bank account on a system that did not support these semantics. It is possible that a single invocation of the remote procedure might lead to multiple withdrawals on the server. For a system to support either of these semantics generally requires the server maintain some form of client state such as the timestamp.

**If a system were unable to support either of these semantics**, then such a **system could only safely provide remote procedures that do not alter data or provide time-sensitive results**. Using our bank account as an example, we certainly require "at most once" or "at least once" semantics for performing a withdrawal (or deposit!) However, an inquiry into an account balance or other account information such as **name, address, etc. does not require these semantics**

https://www.google.com.tw/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&ved=0CC4QFjAA&url=http%3A%2F%2Fwww.cs.gsu.edu%2F~cscnaax%2Fsummer%2Fcs4320_6320%2FAssignments%2Fsol1.doc&ei=rqpMU6jUFIaSkQX_uoHABA&usg=AFQjCNGBO5A7ln5oYa2Yj1aJMIjYF58iJg&sig2=okRebCDG4VPA6UFZFYeBcA

3.10

Ans:

Line X : 0, -1, -2, -3, -4
Line Y : 0, 1, 2, 3, 4

3.11

What are the benefits and the disadvantages of each of the following? Consider both the system level and the programmer level.

a. Synchronous and asynchronous communication 

Ans:

A benefit of **synchronous communication** is that it allows a rendezvous between the sender and receiver. A disadvantage of a **blocking** send is that a rendezvous may not be required and the message could be delivered asynchronously. As a result, message-passing systems often provide both forms of synchronization.

Synchronous => blocking

asynchronous => nonblocking

b. Automatic and explicit buffering 

Ans:

**Automatic** buffering provides **a queue with indefinite length**, thus **ensuring the sender will never have to block while waiting to copy a message**. There are no specifications on how automatic buffering will be provided; one scheme **may reserve sufficiently large memory where much of the memory is wasted**. **Explicit buffering** **specifies how large the buffer is**. In this situation, the **sender may be blocked while waiting for available space in the queue**. However, it is less likely that memory will be wasted with explicit buffering.

c. Send by copy and send by reference 

Ans:

Send by copy does not allow the receiver to alter the state of the parameter.
Send by reference does allow it.

A benefit of send by reference is that it allows the programmer to write a distributed version of a centralized application. Java’s RMI provides both; however, passing a parameter by reference requires declaring the parameter as a remote object as well.

d. Fixed-sized and variable-sized messages 

Ans:

The implications of this are mostly related to buffering issues; with fixed-size messages, a buffer with a specific size can hold a known number of messages. The number of variable-sized messages that can be held by such a buffer is unknown.
