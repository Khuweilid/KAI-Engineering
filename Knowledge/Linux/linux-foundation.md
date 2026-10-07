# LINUX FUNDAMENTALS

## 1. What is linux filesystem root/

    - it is the main directory that holds the entirety of the filesystem.
    - it contains all the systems files, directories for running, booting and managing the system.

    ### 1.1. Home directory

     - it is the directory where the system current user and the workspace is located at in tyhe file system.
     - /home/icon or ~

    ### 1.2. pwd

     - It shows your current directory where you are at at the specific moment you type it meaning print working directory.

    ### 1.3. ls -la

     - ls gives you the list of files and directories available in a specific directory.
     - -l makes the command show detailed info showing permissions,owner, group etc
     - -a askes the command to include even the hidden files.

## 2. linux File Permissions

    - this are security protocols or rules used for the file systems to help the information be secured.

                  r = read
                  w = write
                  x = execute

    - there are are 3 types of permission groups that govern;

                  i. Owner - can rwx----
                 ii. Group - can rx---
                iii. Others - can rx---

    - to change permision of a file you use trhe command 'chmod' and give the file specific permissions like;

                 * chmod 600 private.txt
                 * chmod 644 public.txt
                 * chmod 700 script.sh

        N.B
           600 - gives permision to read and write only to the owner of the file while no access to groups and others.
           644 - Gives the owner permission to read and write in the file but read only access to groups and others.
           700 - gives the owner permision to read, write and execute permisions and no access completely to groups and others.

## 3. Users and Groups

    - the foundation of security,
    - users and groups are used by linux to control ownership and access to files, process, and system resources.

       root user with UID 0, usually has the full access without restrictions.
       while reguler users accounts commonly use UIDs starting from 1000, although the exact allocation depends on the system
       non human  accounts like the systems or services are assigned UIDs 1-999

       Their are two groups Primary and secondary,
       Primary group are assigned to each user during account creation
       secondary groups are the extra additional groups that a user adds for extra permission.

## 4. processes

    - A process is a running instance of a program,
    - this is every instance of when a program is running to execute,
    - usually tracked by the kernel using a unique process-id (PID) PPID and current state.

     ### commands mostly used in processes to get info are;

        'ps' - shows processes associated with the current session.
        'ps aux' - shows you a much broder process listing.
        'pgrep -a <name>' - finds process by name
        'top/htop' - it shows you a live process moniter to see different information of the system.
        'uptime' - shows you for how long the system has been running and load information.
        'lsblk' - shows you the list of block devices such as disks & partitions.
        'ip addr' - shows you linux network interfaces and their ip addresses.
        'echo $$' - displays the PID of the current terminal/bash shell.
        'jobs' - shows all background jobs started from the current shell.
        'kill <PID>' - sends a signal to a process.

    ### 4.1. Parent and child processes
     - process can have relationship with other process to work together.
     - like;

            * PID - process ID
            * PPID - Parent process ID

     - A parent process can create a child process,
     - The PPID becomes the PID of the process that started it.

    ### 4.2. Process hierarchy

     - processes can have parent and child relationships
        like;

                Bash
                  |___ sleep

     - bash shell start sleep process making bash the parent process

    ### 4.3. Background Processes

     - Adding '&' to a command runs the process in the background giving you access to the terminal.
     - Like running;

            ''''bash

                    'sleep 300 &'

            ''''

     - This will allow the terminal to remain available while the process continue running

## 5. Process controll and background jobs

    - running;

        ''''bash

              'ps -p PID -o pd,ppid,user,stat,etime,cmd'

        ''''

      * can be used to inspect a specific process using the process PID.

    ### 5.1 Background processes

     - 'command &' tells the command to run in the background.
     - 'jobs' - this shows you background jobs managed by your current shell.
     - 'pgrep -a process_name' - is or can be used to find a process and its PID.

    ### 5.2 process controll/termination

     - 'kill PID' - sends 'SIGTERM' telling the process to terminate cleanely
     - 'kill -9 PID' - sends 'SIGKILL' telling the process to terminate immidiately (Not first option)

    ### 5.3 Forground and Background processes

     - a forground process takes over the current terminal,
     - using 'Ctrl + z' will suspend the forground process.
     - 'bg' - this will continue a suspended process in the background.
     - 'fg' - will bring the background job back to the forground.
     - '%1' - refers to the job numberin the current shell.

## 6. CPU usage and Scheduling

    - how a CPU is utilized depends with how intensive the process is.
    - a single-threaded CPU-intensive process will use approximately one logoical processor without necessarily using the whole CPU.

      scenario;

         ''''bash

                yes > /dev/null &

         ''''

      - this creates a continous process that performs work without filling the terminal with output directs it to /null which acts as systems blackhole.

            'yes'- will continously generates 'y' output in the terminal
            '> /dev/null' - will discard the output
            '&' - runs the process in the background

      - to observe the process i run;

          ''''bash

                ps -p PID -o pid,ppid,user,stat,%cpu,%mem,etime,cmd

          ''''

      - then used;

          ''''bash

                htop

          ''''

     ### 6.1. load avarage

      - load avarage gives an indication of the amount of work the system is dealing with.
      - running;

          ''''bash

                uptime

          ''''

      - this will display load avarage over approximately:

                 i. 1 minute
                 ii. 5 minutes
                 iii. 15 minutes

## 7. Process Vs Threads

    * Process;
             - it is a running instance of a given program.
             - it has its own resources and address space managed by the OS.

    * Thread;
            - is an execution path in a process.
            - a process can contain multiple threads which share resources and work concurently.

    ### 7.1. commands to see number of threads of a process
     - running;

          ''''bash

               ps -p PID -o pid,nlwp,cmd

          ''''

     - this will show you the number of lightweight process (nlwp) which is used in linux to show threads in a process.
     - running;

          ''''bash

               ps -T -p PID

          ''''

     - this shows the threads belonging to a specific process.

## 8. Concurrency Vs Parallelism

    * Concurrency;
                 - this is when multiple tasks are in progress during the same time but dont necessarily execute at the same time,
                 - the CPU can rapidly switch between the tasks.

    * Parallelism;
                 - this is when multiple tasks execute at the same time on different CPU execution resources.
## 9. Process States

    - Linux process can exist in different states depending on what it is currently doing.
    - Different common process states are;

                                         i. - S = Interreptible sleep/waitting
                                         ii. -R = Running or runnable
                                         iii. -D = Unintarraptible sleep, usually waiting for I/O
                                         iv. - T = Stopped or suspended
                                         v. - Z = Zombie process

    - In 'ps' the STAT collumn shows the process state.
    - The linux kernel continously manages the process and decides which processes recieve CPU time.

## 10. Signals

    - These are small notifications that the linux kernel or processes use to send to a process for control.
    - running the command;

                    ''''bash

                           kill

                    ''''

    - does mot necessarily destroy the process but rather sends a signal to the process on what it should be done.
    - running;
               kill -l
    - this will give you all the signals that linux use for the process.

    ### 10.1. Commonly known signals.

     - there are different types of signals some are;
                              i. SIGHUP - 1 - Hangup
                             ii. SIGINT - 2 - interrupt
                            iii. SIGKILL - 9 - forcefully kill
                             iv. SIGTERM - 15 - request termination.
                              v. SIGSTOP - 19 - stop/pause
                             vi. SIGCONT - 18 - continue/resume

     - when stopping a running forground process using " CTRL + C " sends;

                         SIGINT (2)

     - signal to the foreground process to interupt it.
     - using " CTRL + Z " will send;

                         SIGSTP (19)

     - signal to the foreground process to stop/pause.

     - Unlike 'SIGTERM -15', 'SIGKILL -9' a process cannot catch,ignore, or handle.
     - 'SIGTERM' will ask the process to clean up well before terminating.
     - 'SIGKILL' will terminate the process immediately.

      N.B
         only use (SIGKILL -9) when a process is harmfull.

## 11. Process priority

    - many processes want CPU time.
    - for linux to decide which process gets CPU time and how much prefrence does each process have?
    - Process priority and nice values are introducd.

    ### 11.1. Nice values

     - Linux process have nice values which are used to show CPU time priority.
     - The default value for nice is;

                 nice = 0

      #### 11.1.1. Nice value range to care about.

        - -20 <- higher CPU scheduling priority
        -  0  <- normal
        - +19 <- lower CPU scheduling priority

       N.B
        Negative Nice values have permission restriction around.

     - nice + values will have less priority in the CPU time.
     - nice with - values will have higjh or more priority in the CPU time.
     - to see 'nice values' of a process you use,

         ''''bash

              ps -p PID -o pid,ppid,ni,pri,%cpu,stat,cmd

         ''''

     - where;

             'ni' - will show you the nice values of the process
             'pri' - will give you the priority scheduler.

    ### 11.2. Priority experiment.

     scenario;

     - create 3 intensive high usage CPU processes with different nice values;

              (i) nice -n 10 yes > /dev/null &
             (ii) nice -n 5 yes > /dev/null &
            (iii) yes > /dev/null &

     - 2 process have lower priority since they have high nice values which gives them lower priority in CPU time.
     - the 'yes > /dev/null &' has a normal/default (0) nice value of the three which is the lowest hence gets the highest priority in CPU time.

     - find the processess by running;

           ''''bash

                pgrep -a yes

           ''''

     - then find their details, nice values, priority sceduler,stats by running;

           ''''bash

                ps -C yes -o pid,ppid,ni,pri,%cpu,stat,cmd

           ''''

     - this will give you results;

                    PID    PPID  NI  PRI  %CPU  STAT  CMD
                    614    347   10   9   103   RN    yes
                    615    347    5  14   103   RN    yes
                    618    347    0  19   103   R     yes

     - this shows that high or more nice value has less priority scheduling
     - and low or less nice values have a higher priority scheduling
     - the status 'RN' that the process is running with a modified/niced sceduling priority.
     - the %CPU show (103) showing that the "yes" processes were running with a high CPU consumption.
     - check the systems load avarage by running;

           ''''bash

                  uptime

           ''''

     - which will give you an increased load avarage since the three process are highly consuming the CPU.

             e.g; 1.74  0.74  0.39

     - as per the load avarage of the system;

              = 1.74 → average over 1 minute
              = 0.74 → average over 5 minutes
              = 0.39 → average over 15 minutes

     - after seeing how priority is scheduled for the processess, kill the experiment;
     - running;

            ''''bash

                    pkill yes

            ''''

     - which sends a 'SIGTERM' signal telling the system to terminate all the process associated with 'yes' successfully.

    ### 11.2. renice

     - nice is commonly used when starting a process with a chosen nice value.
     - renice changes the nice value of an already running process.
     - like running;

            ''''bash

                    renice 10 -p PID

            ''''

     - this will change the nice value of a given process PID to '10'

## 12. Linux services & System Processes

     - we ask what happens when Linux needs processes running continously in the background to provide services?
     - A process is a running instance of a program with a unique PID, its own mmeory space, and may contain multipple threads.
     - While a service is an instance of a long-running process usually started by the OS during boot.
     - Services usually run in the background without direct interaction with user.
     - Services provide System-wide functionality 'NETWORKING', 'PRINTING', & 'SCHEDULING'.
     - Examples;

                secure shell daemon (SSHD)
                web server (HTTPD)
                scheduler (CRON)
                logging services

     - Servivecs are background process providing system functionality.
     - also called DAEMONS.

     - when linux starts, many things need to happen for the system to be usable;

                        Computer starts
                               ↓
                      Linux kernel starts
                               ↓
                        systemd starts
                               ↓
                 systemd starts/manages services
                               ↓
                Services create/manage processes
                               ↓
                     System becomes usable


    ### 12.1 What is systemd & systemctl

     - 'systemd' is the init system and service manager used in most modern linux processes.
     - its usually the first process (PID 1) started by the kernel during boot.
     - 'systemd'job is to launch and manage processes and services, handles dependancies, and keeps the system running smoothly.
     - it decides which sevice statrs in whats order, and keeps them running.

     while;

     - 'systemctl' is a command-line tool used to intaract with 'systemd' by letting you start, stop, restart, enable, disable, and check the status of services.
     - in short 'systemctl' is remote control used to tell 'systed' what to do.

    ### 12.2 inspecting system manager

     - run;

        ''''bash

                systemctl is-system-running

       ''''

     - which asks the system manager in what states its in.
     - giving a possibility results of;

                    running
                    degraded
                    starting
                    stopping
                    offline

     - then running;

          ''''bash

               systemctl list-units --type=service --state=running

          ''''

     - will show you the current running service units
     - while ruuning;

         ''''bash

               systemctl list-units --type=service

         ''''

     - will give you all the services that 'systemd' knows about regardles of the state.

## 13. Blueprint on how Linux process work

                              LINUX PROCESS
                                    │
                       ┌────────────┼────────────┐
                       ↓            ↓            ↓
                      PID          PPID         State
                       │            │            │
                     identity      parent       R/S/T
                       │
                       ↓
                    Signals
                       │
                  ┌────┼────┐
                  ↓    ↓    ↓
                STOP CONT TERM
                       │
                       ↓
                   Scheduling
                       │
                   Nice value
                       │
                       ↓
                 CPU preference
                       │
                       ↓
                  CPU usage
                       │
                       ↓
                 Load average




##  what i have learned

    - how linux file system and commands work,
    - how to navigate throgh linux.
    - learned how diffrent systems connect together to work into a one common goal.
    - i also learned diffrent users and groups and how to create permissions.
    - Linux does not simply run programs directly, the OS manages the programs as process and assaigns each process with a unique PID.
    - Monitering processes identifying them with PPID and PID, running processes in the background and terminating the processes.
    - How to observe, control, suspend,resume, and teminate processes from the terminal.
    - processes compete for CPU resources and the operating systems manages which process get CPU time.
    - CPU utilization and system load are related but not the same thing.
    - A program is not the same as a process rather its the source code or executable.
    - A program becomes a process when the OS runs the program.
    - the command KILL does not destroy the process but sends a signal.
    - linux kernel and process use signals to communicate with the processes.
    - Use (SIGKILL -9) only when a process is harmfull or dosent want to close.

##  Problems i encounterd.

    -

##  Questions i still have. 

    -

## What I have learned

The main thing I have learned is that Linux is managing resources and running components as a system.

I started with files and permissions, then moved to users, processes, threads, signals and services.

This gives me a foundation for understanding servers, networking, containers and automation later.

## Status

Completed and practiced.

Detailed experiments are in `Labs/Linux/`.
