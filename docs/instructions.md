# COMPSCI 230 Computer Systems Principles
# Binary Bomb

[download]: https://github.com/umass-cs-230/binary_bomb_project/archive/master.zip

## Overview

In this project you are provided a binary compiled for a 32-bit IA32
Linux environment.  You are *not* provided the C source code for the
compiled binary.  The binary bomb consists of five phases that you
must *defuse* - or the bomb will explode.  When you run the bomb it
will wait for input from the command line.

The binary bomb can be defused by providing the proper input for each of the
five phases.  To defuse a single phase you must type in one or more single
letters or positive decimal numbers, separated by spaces, and hit `enter`.  If
the input is acceptable for that phase the bomb *will not explode*.  If you
provide incorrect input the bomb *will explode* and the program will exit.
You may type up to 5 letters (uppercase or lowercase) or numbers on each line
to defuse each phase.  Here is a successful defusing of a bomb:

```bash
$ ./defuse tdr
phase-1: 4
OK
phase-2: x y z d
OK
phase-3: 9 45
OK
phase-4: v
OK
phase-5: y 3
OK
```

Input that you provide comes after `phase-n:` where `n` is the phase number.
Each of the above input lines correspond to a sequence of characters or
positive integers that can be used to defuse each phase.  That is, `4`
corresponds to phase 1, `x y z d` corresponds to phase 2, etc.  Your goal is
to successfully provide the proper sequence of characters or numbers for each
phase to defuse the bomb and save the world!

Please [download] this project to begin defusing your bomb.

## Review

Before you begin this project it will be helpful for you to review the
material that was covered in class. In addition, you should take a
look at [this](https://youtu.be/75gBFiFtAb8) short video that reviews
what assembly is, how the heap and stack work, and some basics of the
instructions. Do note, however, that this video uses a different
assembly syntax than we did in class. In particular, the order of the
instruction operands are reversed. The video is excellent, but do not
let that confuse you when you look at the assembly in your executable!

## Tools

To be successful in this lab you will need to use tools that we have
covered in class. In particular, you will need to use `objdump` and
`gdb`. The `objdump` tool will disassemble your bomb so you can see
the machine code and assembly of your binary. The `gdb` (GNU Debugger)
allows you to debug a running program. We have provided two scripts,
`debug` and `disassemble` that wrap each of these tools respectively
to make it a little easier to debug your specific bomb. We encourage
you to look at the contents of these scripts to understand how they
work. This is how you use these scripts/tools:

`./disassemble NETID`: Disassembles the binary and generates the
assembly listing to standard output.  You can capture the output with
the following command: `disassemble NETID > bomb-asm.txt`.  This is
useful for looking over the assembly code to get an understanding of
where things are located (i.e., what are the function names that you
might want to use in `gdb` to set a breakpoint).
			  
`./debug NETID`: Runs the bomb in the `gdb` debugger.  This is useful
for inspecting the values of memory and registers as well as control
flow.  You should do the former first and then use `gdb` to inspect
the running program.  Here are some of the `gdb` commands that you may
find useful:

* `info registers`: This will show the current contents of the registers.
  Great when you need to determine the value of a result of executing an
  instruction.  The abbreviation `i r` is convenient.

* `si`: This will step a single instruction (it is short for `stepi`). This is
  useful to go instruction by instruction looking at the contents of your
  registers and memory.
				
* `break <function>`: This will cause execution to break (stop) when you
  arrive in a particular function.  In fact, you can also provide `break` an
  address and it will break just before the instruction at that address.  You
  can abbreviate `break` with `b`. You can also use `break` to stop at
  the start of a particular function. For example, to break at the
  start of your binary bomb you can use `break main`.
				
* `disassemble <function>`: This will disassemble a function.  This is useful
  to see where you are in a particular function.  You will notice the arrow
  (`=>`) before the address of an instruction on the left-hand side - this is
  the instruction your program is about to execute.  You can abbreviate with
  `disas`.

If you find that you need additional information when you are using `gdb` you
should consult `gdb`'s online help system by typing in `help`, ask a question
on the discussion forum, or Google your question.  Google is great for finding
out what a particular ia32 instructions does, for example.  (It is also
possible to download the Intel instruction set manuals, but they are big and
take a bit of wandering around to see how they are organized.) To give
you some help, here are a couple of videos that you should watch
before working on this project to get a better idea of how to inspect
your program with `gdb`:

* [Introduction to GDB a Tutorial](https://youtu.be/sCtY--xRUyI): this
  is a short tutorial on how to use `gdb` to debug a program that has
  including debug symbols. This will help you with the general
  debugging process in other projects. However, in this project we
  need to debug your bomb at the assembly level.
* [GDB Debugging - Displaying x86
  Assembly](https://youtu.be/wIuZajISL-E): this is a short tutorial
  that will help you understand how to inspect a program in execution
  at the instruction level. This will be very helpful in being able to
  understand what the values of the registers are as well as what the
  values of local variables and function arguments are at specific
  locations on the stack.

## Bomb Details

Each bomb is customized for a person attempting this project.  That
is, the input values to defuse the bomb will be different for
everyone.  However, the machinery (algorithms) in each bomb is the
same. To begin the project you simply need to run the provided
`defuse` script and type in your netid (the username you use to login
to Spire and Moodle as well as the username used for your umass email - `NETID@umass.edu`).

The bomb is implemented in 5 phases and each phase must be defused before
proceeding to the next.  If you accidentally "detonate" your bomb you will
receive a message and the program will exit.  It will also write out your
current solution to a `solution.txt` file.  You can use this file to reference
what you typed in to defuse a phase.  BE CAREFUL: the `solution.txt` file will
be overwritten the next time you run the bomb - so if you want to save a
correct solution make sure you copy it to another file before executing the
bomb again (or write the current solution down somewhere).  When you are able
to defuse all phases the generated `solution.txt` file is what you are to
submit to Moodle.  If you are unable to defuse all phases the `solution.txt`
file will record your solution up to the phase you completed.

## Grading

The phases will be graded according to their difficulty level:

* phase-1 : 1 points
* phase-2 : 2 points
* phase-3 : 3 points
* phase-4 : 4 points
* phase-5 : 3 points

Total number of points that you can score: 13

Ultimately, your score will be automatically determined by your
`solutions.txt` file submission.

## Questions

You should use the online discussion forum associated with this project to ask
and answer questions about the bomb and its five phases.  If you are stuck you
should not hesitate to ask for help!  This could be as simple as "Where should
I start?" or as complicated as "Which `gdb` command should I use to view the
contents of the register %eax?".  **Please use the discussion forums to your
advantage**!

You may not ask questions such as "What is the algorithm in phase 3?"
However, you could ask a question such as "I understand phase 3, but can't
seem to get anywhere. Help please".  An acceptable response might be, "Pay
attention to the %eax register".

## HINTS

Start early!  Start simple!  Identify where the phases are in the binary.  Try
to vaguely sketch what the C code might look like (is there an if-else, a
while-loop, a for-loop, etc.).  Identify the number of inputs a phase requires
(there is the easy way, and then there is the hard way).  Run through a phase
several times in `gdb` - find where your input values are - identify which
registers and memory locations hold the letters and/or numbers you type in for
a phase.  Identify if a phase is expecting a number of a character (hint:
remember characters are 1 byte in length and are encoded by ASCII).  For
convenience, here is the chart in hexadecimal and decimal:

```
          2 3 4 5 6 7       30 40 50 60 70 80 90 100 110 120
        -------------      ---------------------------------
       0:   0 @ P ` p     0:    (  2  <  F  P  Z  d   n   x
       1: ! 1 A Q a q     1:    )  3  =  G  Q  [  e   o   y
       2: " 2 B R b r     2:    *  4  >  H  R  \  f   p   z
       3: # 3 C S c s     3: !  +  5  ?  I  S  ]  g   q   {
       4: $ 4 D T d t     4: "  ,  6  @  J  T  ^  h   r   |
       5: % 5 E U e u     5: #  -  7  A  K  U  _  i   s   }
       6: & 6 F V f v     6: $  .  8  B  L  V  `  j   t   ~
       7: ´ 7 G W g w     7: %  /  9  C  M  W  a  k   u  DEL
       8: ( 8 H X h x     8: &  0  :  D  N  X  b  l   v
       9: ) 9 I Y i y     9: ´  1  ;  E  O  Y  c  m   w
       A: * : J Z j z
       B: + ; K [ k {
       C: , < L \ l |
       D: - = M ] m }
       E: . > N ^ n ~
       F: / ? O _ o DEL
```

## Submission Instructions

The submission instructions for this project are simple. Submit the
generated `solution.txt` file to Gradescope. If you do not completely
defuse the binary bomb before the due date you should still submit the
`solution.txt` file for partial credit. You can re-submit your
solution as many times as you wish to Gradescope before the due date
of the assignment.