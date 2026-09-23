# Linux Foundation

## Why I am learning Linux

As a foundation for systems engineering. I will use Linux for servers, automation, containers, networking, AI infrastructure and IoT gateways
by trying to understand what the operating system is doing.

## 1. Filesystem and paths

Linux has a filesystem starting from `/`.

By learning the difference between the root directory and my home directory and how to move around using absolute and relative paths.

Commands I practiced included:

`pwd` shows where I am.

`ls` shows what is in a directory.

`cd` changes my current directory.

The important thing I learned is that my current location affects how relative paths work.

## 2. Permissions

Linux controls access using users, groups and permissions.

The basic permissions are:

- `r` - read
- `w` - write
- `x` - execute

The permission model is based around owner, group and others.

This matters because services and users should not automatically have access to everything on a system.

## 3. Users and groups

Users represent accounts on the system and groups allow permissions to be managed for multiple users.

The basic relationship is:

User → Group → Permissions → Resource access

This becomes important later when I work with servers, services and automation.

## 4. Processes

A process is a running instance of a program.

Linux gives each process a PID.

To inspect processes using:

```
     - bash
ps
ps aux
pgrep

```

I also learned about PID, PPID, process state and parent/child processes.

## 5. Foreground and background jobs

move jobs between foreground and background using:

```
     - bash
jobs
bg
fg

```

I also used `Ctrl+Z` to stop a foreground job temporarily.

I learned that `Ctrl+Z` sends `SIGTSTP`.

## 6. CPU and process experiment

use:

```
      - bash
      
yes > /dev/null &

```

to create a process that continuously used CPU.

then observed the process and stopped it.

This helped me connect a running process to actual system resource usage.

## 7. Threads and concurrency

A process can contain multiple threads.

use:

```
        - bash
        
ps -T

```

and:

```
       - bash
       
ps -p PID -o pid,nlwp,cmd

```

to inspect threads.

The important idea is:

Process → Threads → Concurrent execution

This becomes useful later for servers, AI workloads and other systems that perform multiple tasks.

## 8. Signals

Linux uses signals to control or communicate with processes.

Important signals I practiced:

- `SIGINT` 2
- `SIGTERM` 15
- `SIGKILL` 9
- `SIGSTOP` 19
- `SIGCONT` 18
- `SIGTSTP` 20

`SIGTERM` is a normal request for a process to terminate, while `SIGKILL` forces termination and should be used when normal termination is not working.

## 9. Process priority

I practiced:

```
       - bash
nice
renice

```

This introduced me to process scheduling and priority.

The bigger idea is that the operating system has to manage competing workloads for CPU resources.

## 10. systemd and services

modern Linux systems commonly use systemd as the system and service manager.

A simplified model is:

Kernel → PID 1 → systemd → services → processes

used:

```
       - bash

systemd --version
systemctl
pstree

```

to inspect the system.

## 11. Service lifecycle

I used a service such as cron to observe the lifecycle.

I saw that stopping a service can remove its running process, and starting it again creates a new process with a new PID.

This helped me understand that a service/unit is not the same thing as one permanent process PID.

The service can continue to exist as a managed unit while the process implementing it changes.

## What I have learned

The main thing I have learned is that Linux is managing resources and running components as a system.

I started with files and permissions, then moved to users, processes, threads, signals and services.

This gives me a foundation for understanding servers, networking, containers and automation later.

## Status

Completed and practiced.

Detailed experiments are in `Labs/Linux/`.
