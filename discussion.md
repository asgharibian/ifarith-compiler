# Discussion and Reflection


The bulk of this project consists of a collection of five
questions. You are to answer these questions after spending some
amount of time looking over the code together to gather answers for
your questions. Try to seriously dig into the project together--it is
of course understood that you may not grasp every detail, but put
forth serious effort to spend several hours reading and discussing the
code, along with anything you have taken from it.

Questions will largely be graded on completion and maturity, but the
instructors do reserve the right to take off for technical
inaccuracies (i.e., if you say something factually wrong).

Each of these (six, five main followed by last) questions should take
roughly at least a paragraph or two. Try to aim for between 1-500
words per question. You may divide up the work, but each of you should
collectively read and agree to each other's answers.

[ Question 1 ] 

For this task, you will three new .irv programs. These are
`ir-virtual?` programs in a pseudo-assembly format. Try to compile the
program. Here, you should briefly explain the purpose of ir-virtual,
especially how it is different than x86: what are the pros and cons of
using ir-virtual as a representation? You can get the compiler to to
compile ir-virtual files like so: 

After working on the project with my group mate, we noticed several pros and cons when implementing our code. One common advantage we found is that IR-virtual is easier to read than assembly. Understanding basic things such as arithmetic in assembly isn’t intuitive. However, a con that my group mate and I agree upon is that test cases are harder to implement. In previous personal and class projects, our test cases have been in Python, which is a standard language and easier to understand. Another con that we have encountered is that running the program isn’t straightforward. We have to go through multiple steps to print a result. Finally, one last pro my group and I agree upon is that IR-virtual is way more intuitive to implement, even though producing test cases is harder. Implementing the physical code isn’t as challenging.

hundred.irv: ((mov-lit r0 100) (print r0))

my_sum.irv: ((mov-lit r0 10)
  (mov-lit r1 20)
  (mov-lit r2 0)
  (add r2 r1)
  (add r2 r0)
  (print r2))
  
minus.irv: ((mov-lit r0 20)
  (mov-lit r1 10)
  (mov-lit r2 0)
  (sub r2 r1)
  (sub r2 r0)
  (print r2))


[ Question 2 ] 

For this task, you will write three new .ifa programs. Your programs
must be correct, in the sense that they are valid. There are a set of
starter programs in the test-programs directory now. Your job is to
create three new `.ifa` programs and compile and run each of them. It
is very much possible that the compiler will be broken: part of your
exercise is identifying if you can find any possible bugs in the
compiler.

For each of your exercises, write here what the input and output was
from the compiler. Read through each of the phases, by passing in the
`-v` flag to the compiler. For at least one of the programs, explain
carefully the relevance of each of the intermediate representations.

For this question, please add your `.ifa` programs either (a) here or
(b) to the repo and write where they are in this file.



2.)
This is the asm conversion for  (if 1(print (+ 1 (* 2 3))) (print (- 1 (+ 3 4))))
X86:
section .data
	int_format db "%ld",10,0
	global _main
	extern _printf
section .text
_start:	call _main
	mov rax, 60
	xor rdi, rdi
	syscall
_main:	push rbp
	mov rbp, rsp
	sub rsp, 224
	mov esi, 1
	mov [rbp-64], esi
	mov esi, 0
	mov [rbp-24], esi
	mov edi, [rbp-24]
	mov eax, [rbp-64]
	cmp eax, edi
	mov [rbp-64], eax
	jz lab1267
	jmp lab1273
lab1267:	mov esi, 1
	mov [rbp-56], esi
	mov esi, 2
	mov [rbp-48], esi
	mov esi, 3
	mov [rbp-16], esi
	mov esi, [rbp-48]
	mov [rbp-40], esi
	mov edi, [rbp-16]
	mov eax, [rbp-40]
	imul eax, edi
	mov [rbp-40], eax
	mov esi, [rbp-56]
	mov [rbp-112], esi
	mov edi, [rbp-40]
	mov eax, [rbp-112]
	add eax, edi
	mov [rbp-112], eax
	mov esi, [rbp-112]
	lea rdi, [rel int_format]
	mov eax, 0
	call _printf
	mov rax, 0
	jmp finish_up
lab1273:	mov esi, 1
	mov [rbp-104], esi
	mov esi, 3
	mov [rbp-96], esi
	mov esi, 4
	mov [rbp-88], esi
	mov esi, [rbp-96]
	mov [rbp-32], esi
	mov edi, [rbp-88]
	mov eax, [rbp-32]
	add eax, edi
	mov [rbp-32], eax
	mov esi, [rbp-104]
	mov [rbp-80], esi
	mov edi, [rbp-32]
	mov eax, [rbp-80]
	sub eax, edi
	mov [rbp-80], eax
	mov esi, [rbp-80]
	lea rdi, [rel int_format]
	mov eax, 0
	call _printf
	mov rax, 0
	jmp finish_up
finish_up:	add rsp, 224
	leave 
	ret 

This is the asm conversion for  (+ 5 6)
section .data
	int_format db "%ld",10,0
	global _main
	extern _printf
section .text

_start:	call _main
	mov rax, 60
	xor rdi, rdi
	syscall


_main:	push rbp
	mov rbp, rsp
	sub rsp, 48
	mov esi, 5
	mov [rbp-24], esi
	mov esi, 6
	mov [rbp-16], esi
	mov esi, [rbp-24]
	mov [rbp-8], esi
	mov edi, [rbp-16]
	mov eax, [rbp-8]
	add eax, edi
	mov [rbp-8], eax
	mov rax, [rbp-8]
	jmp finish_up
finish_up:	add rsp, 48
	leave 
	ret 
 
This is the asm conversion for  (- 10 5)
section .data
	int_format db "%ld",10,0
	global _main
	extern _printf
section .text

_start:	call _main
	mov rax, 60
	xor rdi, rdi
	syscall
_main:	push rbp
	mov rbp, rsp
	sub rsp, 48
	mov esi, 10
	mov [rbp-24], esi
	mov esi, 5
	mov [rbp-16], esi
	mov esi, [rbp-24]
	mov [rbp-8], esi
	mov edi, [rbp-16]
	mov eax, [rbp-8]
	sub eax, edi
	mov [rbp-8], eax
	mov rax, [rbp-8]
	jmp finish_up
finish_up:	add rsp, 48
	leave 
	ret 


[ Question 3 ] 

Describe each of the passes of the compiler in a slight degree of
detail, using specific examples to discuss what each pass does. The
compiler is designed in series of layers, with each higher-level IR
desugaring to a lower-level IR until ultimately arriving at x86-64
assembler. Do you think there are any redundant passes? Do you think
there could be more?

In answering this question, you must use specific examples that you
got from running the compiler and generating an output.

ifarith code: 
raw arithmetic file sent for operation. It retains the essential structure of the original code but eliminates certain constructs. The code is in prefix form, and set to work in languages such as racket that evaluate expressions in prefix form.
(if (> 3 2)
    (* 4 5)
    (+ 6 7))

ifarith -> ifarith-tiny
This translates the ifarith code into a simplified version sublanguage called ifarith-tiny the output is essentially the same, taking from the previous file and interpreting it into the sublanguage before further computation is sent to the ANF for further processing. This is to make sure that our compiler is doing arithmetic in the right form so there are no type errors or non prefix functions that would be invalid and not pass through the match cases:
Output:
(if (> 3 2)
    (* 4 5)
    (+ 6 7))
    
ifarith-tiny -> ANF: 
This step converts the simplified ifarith-tiny code into Administrative Normal Form (ANF) for compiler computation. Going out of the compiler, let statements and other forms are added as the expression is converted. This will then be sent to the lower level operation of the computer to complete the computation.
Output:
(let ([x (> 3 2)])
  (if x
      (let ([y (* 4 5)]) y)
      (let ([z (+ 6 7)]) z)))
      
ANF -> IR-Virtual:
In this stage, the ANF code is translated into a linearized list of instructions in Intermediate Representation (IR) Virtual format. This will then be sent to the IR-virtual stage as a list of commands for the computer to add and perform commands programmed through the ANF form.
Output:
((label lab1) (mov-lit x (> 3 2))
 (cmp x 0)
 (jz lab2)
 (mov-lit y (* 4 5))
 (jmp lab3)
 (label lab2) (mov-lit z (+ 6 7))
 (label lab3))
 
IR-Virtual -> x86:
This final stage translates the IR-Virtual instructions into x86 assembly code, which is executable on x86-based architectures in the computer to process a result. This process completes the computation on the lowest level, and results in a numeric output based on the instructions from the ANF to IR-Virtual translation.
Output:
global _main
extern _printf
section .text
_main:
    mov esi, 1 ; result of comparison (> 3 2)
    cmp esi, 0
    jz lab2
    mov esi, 20 ; result of (* 4 5)
    jmp lab3
lab2:
    mov esi, 13 ; result of (+ 6 7)
lab3:
    lea rdi, [rel int_format]
    mov eax, 0
    call _printf
    mov rax, 60
    xor rdi, rdi
    syscall


[ Question 4 ] 

This is a larger project, compared to our previous projects. This
project uses a large combination of idioms: tail recursion, folds,
etc.. Discuss a few programming idioms that you can identify in the
project that we discussed in class this semester. There is no specific
definition of what an idiom is: think carefully about whether you see
any pattern in this code that resonates with you from earlier in the
semester.

Fundamentally, this project is an accumulation of all that we have learned throughout the course, meaning there are “idioms” and other elements of previous projects present within the final project. Although the concept of a “sub-” language may have seemed foreign to students at the beginning of the course, the format of the code in the match case concept as a smaller iteration of some bigger language is a natural progression from projects 3 and 4. As the concepts in the class became more complex, the use of smaller conditionals in our coding, such as “if”, became replaced with match cases to recursively pass in expressions until they reach a returnable form or desired result. Probably the most obvious and continued “idiom” is the presence of lambdas. Since the introduction of the lambda calculus in the course, we have used its reduction process along with match cases in a scheme style for computation and representation of applied functions. Although students may associate lambda usage with project 4, as church encoding involves a high understanding of the lambda calculus, lambdas have been used for functional procedures well before then and continue to be used up to the final project. Another notable “idiom” is the arithmetic aspect of racket being in prefix form. Although computations with lambdas may not make it seem obvious without specific primitive identifiers like “= - / *”, racket’s mathematics and procedures are all in prefix form, something that students had to get used to right at the start of the semester. Recursion also well fits the criteria for an idiom well covered and used throughout the class. Recursive functions, accounting for an arbitrary number of arguments and cases, eliminate the need for hard coding every possible case and outcome, and sometimes are impossible to code without. Presented at the general beginning of the course, recursion has been constantly worked with and now mostly used within other functions we learned like match cases to “break down” an argument to some result or to filter some parameter passed through with some argument.


[ Question 5 ] 

In this question, you will play the role of bug finder. I would like
you to be creative, adversarial, and exploratory. Spend an hour or two
looking throughout the code and try to break it. Try to see if you can
identify a buggy program: a program that should work, but does
not. This could either be that the compiler crashes, or it could be
that it produces code which will not assemble. Last, even if the code
assembles and links, its behavior could be incorrect.

To answer this question, I want you to summarize your discussion,
experiences, and findings by adversarily breaking the compiler. If
there is something you think should work (but does not), feel free to
ask me.

Your team will receive a small bonus for being the first team to
report a unique bug (unique determined by me).

One issue or bug that we had was initially using the terminal to run the project. Using ls to read which files are in the directories helps along with using tab to fill out names on the terminal line is an essential debugging skill that makes running code and file searching easier. Putting the test cases in DrRacket has proven to be helpful in debugging our code, along with using the terminal. One bug with the test case is the "if 0" function returning “0” false for an instance of 0.0. Although they have a difference in type, fundamentally they are the same value. Another strange bug is with the "const.ifa" test case using "=" in the let match case where Racket does not use "=" in their code syntax. Although it may compile, there still is a difference in code run. Bug testing is a tedious experience of checking the test cases and trying to find a situation where your code or some input code results in an unexpected case in combination with your program. At first glance, everything may run fine, but it really does take time to digest each test case and how the code you run functions. Type checking and differences in languages make the process more complex, but are usually signs that something might go away.


[ High Level Reflection ] 

In roughly 100-500 words, write a summary of your findings in working
on this project: what did you learn, what did you find interesting,
what did you find challenging? As you progress in your career, it will
be increasingly important to have technical conversations about the
nuts and bolts of code, try to use this experience as a way to think
about how you would approach doing group code critique. What would you
do differently next time, what did you learn?

Working on this project was an interesting combination of concepts from several other classes that all members in the group are actively taking. Beyond the racket coding and lambda usage we've learned from this course, the machine code as well as terminal usage are all parts of other CIS and CSE classes, so it's interesting to reflect on the project knowing previous knowledge of other classes made applying these skills less foreign. Workload dividing and the non-coding aspects of group work were all made easy with communication, and it was nice to be able to tackle an assignment with a group and learn from each other for a change. These non-coding skills will only increase with more multi-person project experiences. As for the project itself, I’m sure most students are used to the match-cased based sublanguage format by now, and the lambda encoding only gets more applicable as we use it project to project. Lambdas may always be a bit tricky at times, so it's nice to use a language with primitives. The other difficulties specifically lie mostly in reading the assembly code (it's never easy or as straightforward as high-level languages) and test cases themselves being less intuitive since we can’t just check the autograder. I think the most important thing learned was how to apply previous knowledge to a new environment. Every student is well aware of cloning the repository into their computer and working on the next cases to pass, but you really have to get over as a computer scientist working with and adding new environments like the terminal cases or x86 code to what you're used to working on to build up your skill repertoire.


