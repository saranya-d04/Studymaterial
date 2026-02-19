# Operating Systems and Processes: Exercises with Solutions

## 1. Process Basics
1. What is a process?
   - An instance of a running program, with its own memory and resources.
2. What is the difference between a process and a program?
   - A program is a passive set of instructions; a process is an active execution of those instructions.
3. Name two ways to create a new process in Linux.
   - Using `fork()` in code, or running a command in the shell.

## 2. Process Lifecycle
1. List the main states in a process lifecycle.
   - New, Ready, Running, Waiting, Terminated.
2. What is a zombie process?
   - A process that has finished execution but still has an entry in the process table.
3. What is an orphan process?
   - A process whose parent has terminated before it.

## 3. Context Switching
1. What is context switching?
   - The act of saving the state of a running process and loading the state of another.
2. Why is context switching important?
   - It allows multitasking and efficient CPU utilization.
3. What information must the OS save during a context switch?
   - CPU registers, program counter, memory maps, and process state.

## 4. Threads
1. What is a thread?
   - A lightweight process; a unit of execution within a process.
2. How are threads different from processes?
   - Threads share memory within a process; processes have separate memory.
3. Give an example where multithreading is useful.
   - Web servers handling multiple requests simultaneously.

## 5. System Calls
1. What is a system call?
   - A request from a user program to the OS for a service.
2. Name three system calls related to process management.
   - `fork()`, `exec()`, `wait()`.
3. What is the purpose of the `fork()` system call?
   - To create a new process (child) from the current process (parent).

## 6. Linux Process Commands
1. What does the `ps` command do?
   - Lists running processes.
2. How do you kill a process in Linux?
   - Using the `kill` command with the process ID.
3. What is the difference between `nice` and `renice`?
   - `nice` sets the priority when starting a process; `renice` changes it for a running process.

## 7. Advanced
1. How does the OS prevent one process from interfering with another?
   - By using process isolation and memory protection.
2. What is preemptive multitasking?
   - The OS forcibly switches between processes to ensure fair CPU usage.
3. What is a race condition?
   - When two or more processes/threads access shared data concurrently, leading to unpredictable results.
