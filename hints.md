# Hints

## Shell scripting
The Unix shell in a programming environment. Shell commands can be grouped into
text files (called shell scripts) and executed sequentially by the shell.
Commonly used flow control structures are supported, e.g. if-them-else, for, and
while.

There two ways to execute a shell script:
* Use `source script1.sh` in the command line, which treats `script1.sh` as a
  plain-text file.
* Make the script file execuatble by `chmod 700 script1.sh` and run it as an
  execuatble `./script1.sh`. The [Shebang](https://en.wikipedia.org/wiki/Shebang_(Unix))
(`#!/bin/bash`) in `script1.sh` tells the shell what interpreter to use to execute
the script (interpreter directive).

You can pass arguments/parameters to your shell script to customize its behavior.
`script2.sh` demonstrate the use of positional parameters.

Your script will be execuated by `bash` in a process, which spawns processes to
run other commands in your script, and all processes share the same standard
output and standard error. To collect data from you script you can redirect the
output to a file, e.g. `./script1.sh > data`.

Checkout the following resources for details:
* http://linuxcommand.org/lc3_learning_the_shell.php
* http://linuxcommand.org/lc3_writing_shell_scripts.php
* http://cli.learncodethehardway.org/book

## Measure time

The Unix [time](https://en.wikipedia.org/wiki/Time_(Unix)) command can be used
to measure the time a process takes, which includes the wall clock time (total
elapsed time), time in user space, and time in kernel/system space.

To measure the time a process spent on a specific task, e.g. memory access, we
have to instrument the code by reading the clock before and after and calculate
the difference as shown in the following examples:
* [time_diff.c](./time_diff.c)
* a [TLB test program](https://github.com/torvalds/test-tlb/blob/master/test-tlb.c)
  written by Linus.

Measuring time can be tricky. You can use `gettimeofday`, `clock_gettime`, and
`clock_getres` with pros and cons.
[Accuracy and precision](http://www.mathsisfun.com/accuracy-precision.html) can
be confusing.

You can also measure time by counting CPU cycles as shown in [rdtsc.c](./rdtsc.c).

As a side note leap seconds can be a factor too if you are 'lucky':
* https://www.timeanddate.com/time/leapseconds.html
* https://docs.oracle.com/javase/8/docs/api/java/util/Date.html
* https://docs.oracle.com/javase/8/docs/api/java/time/Clock.html

## Miscellaneous

### Linux per-thread stack size
```
ulimit -s
8192
```
`8192K=2^13*K=8M` suggests that 8M is the default size
([source](https://unix.stackexchange.com/questions/127602/default-stack-size-for-pthreads)).

### Linux heap size:
```
ulimit -m
unlimited
```

### Handle command line arguments in C
https://www.cs.swarthmore.edu/~newhall/unixhelp/C_commandlineargs.php

### Use logarithmic scale
http://ploticus.sourceforge.net/doc/prefab_stdparms.html

### TLB
https://en.wikipedia.org/wiki/Translation_lookaside_buffer

### Information about CPU architecture
```
man lscpu

sudo apt-get install cpuid
cpuid | grep TLB
```

### Pin a process/thread to a CPU core
```
sudo apt-get install cpuset
```
