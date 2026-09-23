# Linux Foundation Experiments

These are the practical Linux experiments I actually worked through.

## Experiment 1 — Processes and parent/child relationships

### Objective

I wanted to understand that a running program is represented by a process and that processes can have parent and child relationships.

### What I did

I started:

```bash
sleep 300 &
```

Then I used process inspection commands such as:

```bash
ps
ps aux
pgrep -a sleep
pstree
```

### What I observed

The `sleep` command created a running process with its own PID.

I could see the process in the process list and inspect its relationship with its parent.

### What I learned

A process is a running instance of a program.

Linux assigns it a PID and keeps it in a process hierarchy.

### Engineering connection

This matters later when I work with services, containers and server applications.

---

## Experiment 2 — Foreground and background jobs

### Objective

I wanted to understand how Linux handles jobs running in the foreground and background.

### What I did

I started a job, stopped it with:

```text
Ctrl+Z
```

Then checked:

```bash
jobs
```

and used:

```bash
bg
fg
```

### What I learned

`Ctrl+Z` sends `SIGTSTP` and stops the job temporarily.

`bg` continues the stopped job in the background.

`fg` brings it back to the foreground.

### Engineering connection

This helped me understand process/job control instead of treating the terminal as just a place to type commands.

---

## Experiment 3 — CPU usage

### Objective

I wanted to see a process consume CPU resources.

### What I did

I ran:

```bash
yes > /dev/null &
```

Then observed the process using process monitoring tools.

### What I learned

The process continuously generated output, but `/dev/null` discarded it.

The process still consumed CPU because the work was being performed before the output was discarded.

I then stopped the process.

### Engineering connection

This helped me connect processes to actual resource usage and system performance.

---

## Experiment 4 — Threads

### Objective

to see the difference between a process and its threads.

### What I did

I used:

```bash
ps -T
```

and:

```bash
ps -p PID -o pid,nlwp,cmd
```

### What I learned

A process can contain multiple threads.

Threads allow work to be executed concurrently inside the same process.

### Engineering connection

This becomes important for servers, parallel workloads and AI systems.

---

## Experiment 5 — Signals

### Objective

o understand how Linux controls running processes.

### Signals I practiced

```text
SIGINT   2
SIGTERM 15
SIGKILL  9
SIGSTOP 19
SIGCONT 18
SIGTSTP 20
```

### What I learned

Signals provide a way to request or force process state changes.

Learned that:

- `SIGTERM` asks a process to terminate normally.
- `SIGKILL` forces termination.
- `SIGSTOP` stops a process.
- `SIGCONT` continues a stopped process.
- `SIGTSTP` is associated with terminal job suspension such as `Ctrl+Z`.

### Engineering connection

Process control is important for services, automation, containers and fault handling.

---

## Experiment 6 — Process priority

### Objective

to understand how process priority can be changed.

### What I did

I experimented with:

```bash
nice
renice
```

and observed the nice values of processes.

### What I learned

Linux uses scheduling and priority values when managing competing CPU workloads.

### Engineering connection

This becomes useful when managing systems with multiple workloads.

---

## Experiment 7 — systemd and services

### Objective

understand how Linux manages services.

### What I did

I checked systemd:

```bash
systemd --version
```

and inspected the process hierarchy:

```bash
pstree
```

I also used `systemctl` to inspect and manage a service.

### Service lifecycle

I observed a service being:

```text
active
↓
stopped
↓
process disappears
↓
started
↓
new PID
```

I also observed restart behavior.

### What I learned

The service unit is managed independently of the specific process PID currently running it.

### Engineering connection

This is important for servers and infrastructure because production systems need services that can be started, stopped, restarted and monitored.

