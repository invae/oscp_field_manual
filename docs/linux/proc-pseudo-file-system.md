# proc-pseudo-file-system

These entries are most effective for operations within a docker container. These entries should be considered when a means of information disclosure is available. Thorough enumeration of the `/proc` file system arbitrary read can lead to full system compromise.


## /proc/net/tcp

This is where we can find information on the current TCP connections and listening sockets. When tools like `netstat` and `ss` are not included in a container, we can still get information out of this file. Note that address are usually represented in hexadecimal, convert accordingly. 


## /proc/sched/debug

Information on current running processes. Discloses all running services at point of read. 

- process id numbers
- parent PID
- command lines

This entry is great for pivot enumerations. Use this file to determine the PID of a process running on target system, pivot to enumerating `/proc/DISCOVERED_PID`



## /proc/PROCESS_ID/maps

Memory addresses of `PROCESS_ID`. This entry is mission critical if the target binary does not implement address space randomization per thread. Enables address calculations for things such as `libc` strings for return oriented programming exploits. 

- `offset_of_libc_string_in_image + addr_of_libc_in_memory = addr_in_memory`

