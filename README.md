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

You may run the following command to see the difference. The "elapsed time" shown in the stopwatch is always a little less than the real time elapsed. In most cases this small error doen't matter a lot, however you should be aware of the fact!

```
$ run "sleep 10" /
  [running]
  command: 	sleep 10

  $ sleep 10
  ================================ /dev/stdin
  pid		[8214]
  elapsed	0m9.7s
  real		0m10.001s
  user		0m0.000s
  sys		0m0.000s
```

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

## Language Support

| Language        | Recognized extension          | Canonical compiler | Canonical runtime/interpreter |
| --------------- | ----------------------------- | ------------------ | ----------------------------- |
| **C**  | `.c` | `gcc` | |
| **C++** | `.cpp`, `.cc`, `.cxx`, `.c++` | `g++` | |
| **Java** | `.java` | `javac` | `java` |
| **Pascal** | `.pas` | `fpc` | |
| **BASIC** | `.bas` | `fbc` | |
| **Visual Basic .NET** | `.vb` | `vbnc` | `mono` |
| **C#** | `.cs` | `mcs` | `mono` |

Alternatively, you may assign environment variable `IMPL` to specify which implementation to use, e.g. `IMPL=clang++ hit ackermann.cpp`
