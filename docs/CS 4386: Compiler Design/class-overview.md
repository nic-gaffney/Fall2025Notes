# Class Overview
08/25/2025

---
## Grading
- Attendance / Homework: 10%
    - Random Attendance, -1 on final grade from 2nd absence
    - 3 homeworks
- Project: 45%
    - Lexical, Syntax, Semantic analysis
- Exam 1-3: 45% (15% each)
    - Problems similar to homeworks
    - In person during regular lectures
## Exams
Exams are **Not** cumulative, each generally
covering a seperate topic from the others.

## Goals
- Understand common lang processors
- Overview the structure and phases of compilers
- Why study compilers

## What is a compiler?
source $\rightarrow \boxed{compiler} \rightarrow$ target program

A compiler is a program that can read a program in
one language,the source language, and translate it
into an equivalent program in another language,
the target language.

#### Why is there a need for compilers?
- Functionality that may not be available in target language
- Before a program can be run, it must be translated into a form
that can be executed by a computer.
- An important role of the compiler is to report any errors in
the source program that it may detect.
- In general, the compiler should improve the program in some way

## Language Processors
- A compiler is a common type of language processor.
- Interpreter is another common kind
    - An interpreter appears to directly execute operations
    specified on input.

## Compiler vs. Interpreter
- Compiler can generate faster
- Interpreter can give better diagnostics
