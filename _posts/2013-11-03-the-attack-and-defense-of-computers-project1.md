---
layout: post
title: 'The Attack and Defense of Computers : Project1'
date: 2013-11-03 07:44
comments: true
tags: [course, The Attack and Defense of Computers]
---
### Project 1 ###

Description:

Write two programs with the following properties:

On a host, called ***server host*** , write a program, called **password_holder.c** , that allows a user to input a character string.
After obtaining an input string from a user, **password_holder.c** opens a TCP/IP socket and listens on the socket to wait for any incoming request from a host, called client host.
When an incoming connection is established, **password_holder.c** sends the input string to the the client host as a password.

On a host, called ***client host*** , write a program, called **mission_impossible.c** , that connects to the above remote server to retrieve a password.
The compiled executable file of **mission_impossible.c** is called **mission_impossible.exe** .
After obtaining a password from the above server, **mission_impossible.c** asks its users to input a password.

If an input password is identical to the passwrod that **mission_impossible.c** retrieved from the above server, the program will execute a piece of code, called Mission Briefing Code (MBC) hereafter, that will display the following message (" **Ethan Hunt, Run Now!** ") for **2 minutes** and then delete the file **mission_impossible.exe** and terminate itself.

If an erroneous password is input, the program will delete the file mission_impossible.c and terminate itself.

Initially, MBC must be stored in a global array and is encoded with your password. You can use any approach to encode MBC. When the input password is correct, your program will decode MBC and place it in the heap and then transfer your execution flow to the decoded MBC.

Hint:

1. [Grading Criteria and reference meatrial](http://in1.csie.ncu.edu.tw/~hsufh/COURSES/FALL2013/p1_ref_material.pptx)
2. 

- You can write your MBC as a normal program first.
- Then compile the above program.
- Then use a tool, such as objdump, to find the corresponding machine code.

3. You can use your password to XOR the MBC to encode it.

4. You may need to use the library function printf to display message. Hence, in your MBC you may need to know the address of function printf. To simply the problem, use static link to compile your program so that function printf will be inside your executable file and you can use a tool, such as objdump, to find the address of the function.

5. When calling function printf, do not forget to prepare the stack segment correctly so that function printf can obtain its parameters.

## Project Submission:

- The due day of reports submission is **3rd Dec** .
- The demo will be held on **4th Dec** . and **5th Dec** .
- Contact the TAs to choose your demo time before **3rd Dec** .
- On site demo of this project is required.
- When demonstrating your projects, the TAs will ask you some questions regarding to your projects. Part of your project grade is determined by your answers to the questions.
- You need to submit both an electronic version and a hard-copy of your project report to the TAs.
The electronic versions could be sent to the TAs through e-mails.
Do not forget writing the names and student IDs of all members in your team.

Your report should contain:
- Your source code
- the execution results

Late submission will NOT be accepted.