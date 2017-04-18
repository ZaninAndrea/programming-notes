# Chapter 9
<!-- toc -->
## Introduction to processes and process attributes
A process is simply an instance of one or more related tasks (threads) executing on your computer.

| Process Type | Description | Example |
| --- | --- | --- |
|Interactive Processes | Need to be started by a user, either at a command line or through a graphical interface such as an icon or a menu selection. |	bash, firefox, top |
| Batch Processes | Automatic processes which are scheduled from and then disconnected from the terminal. These tasks are queued and work on a FIFO (First In, First Out) basis. | updatedb |
| Daemons | Server processes that run continuously. Many are launched during system startup and then wait for a user or system request indicating that their service is required. | httpd, xinetd, sshd |
| Threads | Lightweight processes. These are tasks that run under the umbrella of a main process, sharing memory and other resources, but are scheduled and run by the system on an individual basis. An individual thread can end without terminating the whole process and a process can create new threads at any time. Many non-trivial programs are multi-threaded. |	firefox, gnome-terminal-server |
| Kernel Threads | Kernel tasks that users neither start nor terminate and have little control over. These may perform actions like moving a thread from one CPU to another, or making sure input/output operations to disk are completed. | kthreadd, migration, ksoftirqd |

The **scheduler** handles a **run queue** of processes, that want to be executed, and allows them to use the CPU. Processes in this queue are said to be in a **running** state, they can also be in a **sleep** state when they wait for some event to happen before they can resume.

The priority for a process can be set by specifying a **nice value**, or **niceness**, for the process. The lower the nice value, the higher the priority. A nice value of -20 represents the highest priority and 19 represents the lowest. (

| ID Type | Description |
|---|---|
| Process ID (PID) | Unique Process ID number |
| Parent Process ID (PPID) | Process (Parent) that started this process. If the parent dies, the PPID will refer to an adoptive parent; on recent kernels, this is kthreadd which has PPID=2. |
| Thread ID (TID) | Thread ID number. This is the same as the PID for single-threaded processes. For a multi-threaded process, each thread shares the same PID, but has a unique TID. |



![](https://d37djvu3ytnwxt.cloudfront.net/assets/courseware/v1/fbe122ffd13edf336ad978cddb953a7f/asset-v1:LinuxFoundationX+LFS101x+1T2017+type@asset+block/LFS01_ch16_screen07.jpg)

## Process metric and process control
The **load average** is a metric for the work-load of the system. E.g. a load average of 0.54 signifies that the system has been 54% utilized on average.
The load average has a scale from 0 to the number of cores. E.g. on a quadcore system a load average of 1 means that 100% of the power of one core has been utilized, the maximum load average possible is 4.

* `w`, `top` or `uptime` also show the load average. `w` shows the load average in the last 1,5,15 minutes.
* `kill -SIGKILL <pid>` or `kill -9 <pid>` to kill a process
* You can put a job in the background by suffixing `&` to the command 
* `jobs -l` to show all background processes
* `fg` and `bg` to move processes to foreground or background

