# hit & run

A simple command-line wrapper to compile, run and timekeep single-file programs more easily. Handy for competitive programming (ACM-ICPC, Google Code Jam, TopCoder, etc.)

## Usage

### #1

Compile and run a program with timekeeping:

```
$ run SOURCE_FILE INPUT_FILE [ARGUMENTS] > OUTPUT_FILE
```

(e.g. `run Foo.java test01.txt > test01.out`)

If no input file is needed by the program, put "`/`" in place. (e.g. `run Foo.java / > test01.out`)

*Note: no compiler options can be passed if used this way.*

### #2

Compile:

```
$ hit SOURCE_FILE COMPILER_OPTIONS
```

(e.g. `hit Foo.java`)

Run a compiled program with timekeeping:

```
$ run PROGRAM_FILE INPUT_FILE [ARGUMENTS] > OUTPUT_FILE
```

(e.g. `run Foo test01.txt > test01.out`)

If no input file is needed by the program, put "`/`" in place. (e.g. `run Foo / > test01.out`)

### Disable timekeeping

The `INPUT_FILE` parameter (or "`/`" if no input file needed), together with the rest of arguments, can be ignored. Doing so will **disable timekeeping** and use **standard input**. As usual, nothing can prevent you from redirecting input from a file, e.g. `run Foo < test01.txt > test01.out`

### A few notes on timekeeping

Firstly, timekeeping is **not guaranteed to be accurate** due to inevitable shell execution overhead. It serves only as a stopwatch so you know roughly how much time has elapsed while running your program.

A *pid* is displayed when timekeeping the program. This process **will not be killed even if you terminate `run` manually**. As it still runs in the background, you may choose to either let it go and finish, or `kill` it explicitly.

## Demo

Measure the running time of computing the [Ackermann function](https://en.wikipedia.org/wiki/Ackermann_function) `A(3,12)` recursively in Java and C++:

```
$ cd samples
$ ../run Ackermann.java / > ackermann.out
$ ../run ackermann.cpp / > ackermann.out
```

Compile the C++ program with optimization first, then measure the running time:

```
$ ../hit ackermann.cpp -O3
$ ../run ackermann / > ackermann.out
```

## Unlicense

This is free and unencumbered software released into the public domain.
