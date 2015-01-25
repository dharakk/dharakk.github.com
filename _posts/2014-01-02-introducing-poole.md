---
layout: post
title: Implementation of Shell using C
---

*Writing your own bash* is as exciting as it sounds! When the prompt of your design answers to your commands like a clockwork, the feeling is something  else. So, I will describe briefly how I did it. 

-----

You can read about the the system calls used in [The GNU C library](http://www.gnu.org/software/libc/manual/html_node/index.html). Before diving in you might want to look at [Input/Output Overview](http://www.gnu.org/software/libc/manual/html_node/index.html#toc-Input_002fOutput-Overview) and [Pipes and FIFO](http://www.gnu.org/software/libc/manual/html_node/index.html#toc-Pipes-and-FIFOs-1).

These are the system calls we will be using:

* fork()
* execvp()
* pipe()
* dup2()
* wait()

In addition to these, there will be a basic parsing mechanism.

### External commands execution:

* What 'execvp()' syscall does is, it replaces the current process image with another process. We will use this and the external binary files to execute all external commands.
* We first parse the user input, clean them of extra white spaces and extract command and the parameters.
* Now we will fork a process and within this child process call 'execvp()' and supply the binary location of the required command and the parameters
* 'execvp()' will replace the child image will that of the command being executed.
* Other than execvp() any other flavour of 'exec()' can be used. Read more about 'exec()' [here](http://pubs.opengroup.org/onlinepubs/009695399/functions/exec.html).

So,the most easy part of shell is done.

### I/O redirection

* 'dup2()' system call will come in handy for this purpose. Basically dup2(int new,int old) duplicates the 'old' descriptor into 'new'.
* Now the job is simple, we open a file and get the file descriptor and depending upon we want input / output redirection, we duplicate stdin/stdout into the file descriptor.

The code would look like this: 

{% highlight cpp %}

int fdi=open(arglist2[0],O_RDONLY);
dup2(fdi,0);

{% endhighlight %}


### Pipeline

For a command pipeline, create a pipe using 'pipe()' system call and duplicate the file descriptors of pipe to stdin/stdout. yes, that simple! For more than one level of pipeline just carefully crafted sequence of 'pipe()' and 'dup2()' command will be required. Do not forget ot close the unused end of the pipe in both the process, this can be a real deal-breaker.

### A little extra

* You can implement internal commands like 'cd' od 'pwd' using 'chdir()' and 'getcwd()' syscalls.
* Basic history command or bang operator can be implemented by just maintaining a history file and modfying the parsing function a little.
* Detect & in the input and do not call 'wait()' for the parent process, this way the child will go into background.

My version of implementation can be found [here](https://github.com/dharakk/nutsh).
















 

Thanks!
