## About

A basic HTTP server written in python that can handle multiple concurrent requests

Basic concepts and steps followed to build this server
 - Use python socket library to create,bind and accept requests on a TCP/IP socket
 - Use fork() system call to create child processes to handle concurrent requests
 - Specify incoming connection request in kernel queue for the server socket to enqueue requests
 - Close client sockets to prevent stale duplicate UNIX file descriptors causing OS to run out of available file descriptors
 - Prevent zombie process creation using asynchronous SIGCHILD handler and wait() system call to collect exit details of child processes created using fork() system call
 - Handle interruptions of system calls - child process existing causing SIGCHILD causing event handler in parent and parant's accept() system call
 - Set up a SIGCHLD event handler but instead of wait use a waitpid system call with a WNOHANG option in a loop to make sure that all terminated child processes are taken care of and nothing is missed in case mulitple child process exit at once

Reference
- https://ruslanspivak.com/