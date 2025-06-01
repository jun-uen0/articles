# SRE Linux Internals Quiz
## 📘 Chapter 1: Shell Internals
### 1. What are the standard file descriptors and what does each represent?
### 2. What happens when you press Ctrl+C in a terminal?
### 3. Which tool is used to trace syscalls for debugging?

## 📘 Chapter 2: File Descriptors
### 4. What's the difference between a file descriptor and an open file description?
### 5. How does dup2() differ from dup()?
### 6. What does the O_CLOEXEC flag do and when is it important?
### 7. Name one way to check if two processes share the same open file description.

## 📘 Chapter 3: Pipes
### 8. What system call is used to create a pipe?
### 9. What signal is triggered when a writer writes to a pipe without readers?
### 10. Why does head in a pipeline cause grep and cat to exit?

## 📘 Chapter 4: Process Groups & Jobs
### 11. What is the difference between a process group and a session?
### 12. What does the tcsetpgrp() syscall do?
### 13. How does nohup prevent a process from termination when the terminal closes?

## 📘 Chapter 5: Terminals & Pseudoterminals
### 14. What's the difference between /dev/tty and /dev/pts/*?
### 15. What does the SIGWINCH signal indicate?
### 16. What tool can move a process into a tmux session after it was started?