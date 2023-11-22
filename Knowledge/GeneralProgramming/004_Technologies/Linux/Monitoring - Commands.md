
#### TOP

Display all the running and active real-time processes in an ordered list and updates it regularly. It displays **CPU usage**, **Memory usage**, **Swap Memory**, **Cache Size**, **Buffer Size**, **Process PID**, **User**, **Command**s

```
top

top -b -o +%MEM | head -n 22 > topreport.txt
```

1. `-b` : runs top in batch mode
2. `-o` : used to specify fields for sorting processes (MEMORY USAGE in this case)
3. `head` utility displays the first few lines of a file and
4. `-n` option is used to specify the number of lines to be displayed.

### VM STAT

Linux **VmStat** command is used to display statistics of **virtual memory**, **kernel threads**, **disks**, **system processes**, **I/O blocks**, **interrupts**, **CPU activity,** and much more.

```
vmstat
```

![[VMSTAT_demo.png]]
### LSOF

The **lsof command** is used in many **Linux/Unix-like** systems to display a list of all the open files and processes. The open files included are **disk files**, **network sockets**, **pipes**, **devices,** and **processes**.

```
lsof (| less)
```

![[LSOF_demo.png]]

### TCPDUMP

The **tcpdump** command is one of the most widely used command-line **[network packet analyzer](https://www.tecmint.com/wireshark-network-traffic-analyzer-for-linux/ "Wireshark to Analyze Packets in Linux")** or **packet sniffer** programs that is used to capture or filter **TCP/IP** packets that are received or transferred on a specific interface over a network.

```
tcpdump -i eth0 port 22
tcpdump -c 5 -i eth0
tcpdump -D
```
 - with `-i` switch only capture from the desired interface
 - using `-c` option, you can capture a specified number of packets.
 - -D Display available interfaces

### Netstat – Network Statistics

The **netstat** is a command-line tool for monitoring **incoming** and **outgoing network** packet statistics as well as interface statistics. It is a very useful tool for every system administrator to monitor network performance and [troubleshoot network-related problems](https://www.tecmint.com/linux-network-configuration-and-troubleshooting-commands/ "13 Linux Network Configuration and Troubleshooting Commands").

```
netstat -a | more
```

![[NETSTAT_demo.png]]
### HTOP  – Linux Process Monitoring

**htop** is a much advanced interactive and real-time Linux process monitoring tool, which is much similar to Linux **[top command](https://www.tecmint.com/save-top-command-output-to-a-file/ "How to Save Top Command Output to a File")** but it has some rich features like a **user-friendly interface to manage processes**, **shortcut keys**, **vertical and horizontal views of the processes,** and much more.

![[HTOP_demo.png]]

### IPTraf – Real-Time IP LAN Monitoring

**IPTraf** is an open-source console-based real-time network (**IP LAN**) monitoring utility for **Linux**. It collects a variety of information such as [IP traffic monitor](https://www.tecmint.com/tcpflow-analyze-debug-network-traffic-in-linux/ "TCPflow – Analyze and Debug Network Traffic in Linux") that passes over the network, including TCP flag information, ICMP details, TCP/UDP traffic breakdowns, TCP connection packets, and byte counts.


![[IPTRAF_demo.png]]


### Monitorix – System and Network Monitoring

**Monitorix** is a free lightweight utility that is designed to run and monitor system and network resources as many as possible in **Linux/Unix** servers.

![[MONITORIX_demo.png]]