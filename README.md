# Performance-monitor-training
Performance Monitor from zero to hero



Absolutely, Noe. As a Windows Server Administrator, Performance Monitor (PerfMon) is one of the most powerful troubleshooting tools you can learn. Most administrators only use Task Manager and Resource Monitor, but PerfMon allows you to identify bottlenecks, prove root cause, baseline server performance, and even predict future capacity issues.

Windows Performance Monitor: From Zero to Hero
What is Performance Monitor?

Performance Monitor (PerfMon) is a built-in Windows tool that allows you to:

Monitor CPU utilization
Monitor memory consumption
Analyze disk performance
Monitor network activity
Identify bottlenecks
Baseline server health
Capture performance data over time
Troubleshoot slow applications
Analyze IIS performance
Diagnose SQL Server issues
Investigate high CPU or memory alerts

Think of PerfMon as the EKG machine for Windows Servers.

Lesson 1: Launching Performance Monitor
Option 1

Press:

Windows + R


Type:

perfmon


Press Enter.

Option 2

Server Manager

Tools
   → Performance Monitor

Understanding The Sections

On the left side you'll see:

Monitoring Tools
   ├─ Performance Monitor

Data Collector Sets
   ├─ User Defined
   ├─ System

Reports


Most administrators work primarily in:

Performance Monitor
Data Collector Sets
Reports

Lesson 2: Add Counters

Open:

Monitoring Tools
   → Performance Monitor


You'll see a graph.

Click:

+


(Plus Sign)

This opens the counter list.

First Counters Every Admin Should Learn
CPU

Expand:

Processor


Select:

% Processor Time


Choose:

_Total


Add.

Memory

Expand:

Memory


Add:

Available MBytes
Pages/sec

Disk

Expand:

Physical Disk


Add:

Avg. Disk Queue Length
Disk Transfers/sec
% Disk Time

Network

Expand:

Network Interface


Add:

Bytes Total/sec


Select your active NIC.

Lesson 3: Understanding Healthy Values
CPU

Counter:

Processor(_Total)\% Processor Time


Healthy:

< 50%


Watch:

70-80% sustained


Action:

Investigate processes.

Memory

Counter:

Memory\Available MBytes


Healthy:

> 1024 MB free


Watch:

< 500 MB free


Critical:

< 250 MB free

Disk Queue

Counter:

PhysicalDisk\Avg. Disk Queue Length


Rule:

Queue Length should not exceed
2 per spindle


Simple rule:

< 2 = good

Pages/Sec

Counter:

Memory\Pages/sec


Healthy:

< 50


Possible memory pressure:

> 100 sustained

Lesson 4: Real-World Troubleshooting

Let's pretend your IIS application users say:

Capture is slow

How do we prove where the bottleneck exists?

Monitor:

CPU
Memory
Disk
Network


At the same time.

If CPU hits:

95%


Problem:

Processor bottleneck


If Memory Available MB:

100


Problem:

Memory shortage


If Disk Queue Length:

15


Problem:

Storage bottleneck


If Network:

Near NIC maximum


Problem:

Network congestion

Lesson 5: The Counters Every Enterprise Admin Uses
CPU Counters
Processor(_Total)\% Processor Time

System\Processor Queue Length

Process(*)\% Processor Time

Memory Counters
Memory\Available MBytes

Memory\Pages/sec

Memory\Committed Bytes

Process(*)\Working Set

Disk Counters
PhysicalDisk(*)\Disk Reads/sec

PhysicalDisk(*)\Disk Writes/sec

PhysicalDisk(*)\Avg. Disk Queue Length

PhysicalDisk(*)\Avg Disk sec/Read

PhysicalDisk(*)\Avg Disk sec/Write

Network Counters
Network Interface(*)\Bytes Total/sec

Network Interface(*)\Output Queue Length

Lesson 6: Identify Which Process Is Causing High CPU

Add:

Process(*)\% Processor Time


This shows:

w3wp.exe
sqlservr.exe
java.exe
tomcat.exe
capture.exe
etc.


You'll immediately see:

Which process is consuming CPU


This is one of the most valuable counters in PerfMon.

Lesson 7: Create a Baseline

A baseline means:

What does normal look like?


Many admins wait until a system is broken.

Experts gather data while the server is healthy.

Record:

CPU average

Memory usage

Disk queue

Network traffic


during:

Normal business hours


Save this information.

Now when an alert occurs:

You can compare

Lesson 8: Data Collector Sets

This is where PerfMon becomes really powerful.

Navigate:

Data Collector Sets
   → User Defined


Right-click:

New
  → Data Collector Set


Name:

Server Health Baseline


Choose:

Create Manually


Add Counters:

Processor(_Total)\% Processor Time

Memory\Available MBytes

Memory\Pages/sec

PhysicalDisk(*)\Avg. Disk Queue Length

Network Interface(*)\Bytes Total/sec


Sample interval:

15 Seconds


Save logs:

C:\PerfLogs


Start collection.

Now PerfMon records performance even when you are offline.

Lesson 9: Analyze Historical Data

Open:

Reports


Find:

Your Data Collector Set


You'll see:

CPU trends

Memory trends

Disk trends

Network trends


You can review exactly what happened overnight.

This is extremely useful for:

Reboots
Application slowdowns
IIS issues
SQL issues
Memory leaks
Lesson 10: Troubleshooting an IIS Web Server

Since you work with IIS migrations and applications, these counters are invaluable.

Add:

Web Service


Counters:

Current Connections

Bytes Sent/sec

Bytes Received/sec


Also Add:

Process(w3wp)\% Processor Time

Process(w3wp)\Private Bytes


Signs of Memory Leak:

Private Bytes continuously grows

Never decreases


Over days:

1 GB
2 GB
4 GB
8 GB


Eventually:

Application Pool crashes

Lesson 11: Monitor a 10GB Network Adapter

Because you've recently been discussing 1GB versus 10GB Capture server connections, monitor:

Network Interface(*)\Bytes Total/sec


Convert:

1 Gig Ethernet

125 MB/sec maximum

10 Gig Ethernet

1,250 MB/sec maximum


PerfMon lets you validate whether your workload actually benefits from the 10GB NIC.

Lesson 12: Create Alerts

Navigate:

Data Collector Sets


Create:

Performance Counter Alert


Examples:

CPU Alert
Processor(_Total)\% Processor Time

Threshold:
90%

Memory Alert
Memory\Available MBytes

Threshold:
500 MB

Disk Alert
PhysicalDisk(*)\Avg. Disk Queue Length

Threshold:
10


When exceeded:

Log Event
Run Task
Send Alert

Lesson 13: Enterprise Troubleshooting Workflow

Whenever a user reports:

The server is slow


Follow this exact order:

Step 1

Check:

CPU


If high:

Determine process

Step 2

Check:

Memory


Look for:

Available MB

Pages/sec

Step 3

Check:

Disk Queue


Storage issues are extremely common.

Step 4

Check:

Network Interface


Look for saturation.

Step 5

Review:

Application Logs


Correlate PerfMon findings with:

Event Viewer

IIS Logs

Application logs

Your First Home Lab Exercise

On one of your Windows Server 2025 test servers:

Create a Data Collector Set

Counters:

Processor(_Total)\% Processor Time
Memory\Available MBytes
Memory\Pages/sec
PhysicalDisk(*)\Avg. Disk Queue Length
Network Interface(*)\Bytes Total/sec


Sampling:

15 Seconds


Duration:

1 Hour


Then:

Open several browser sessions.
Copy a large file.
Run Windows Update scan.
Monitor the counters.
Review the report.

You will quickly learn how CPU, memory, disk, and network interact.

The 10 Counters Every Windows Administrator Should Memorize
Processor(_Total)\% Processor Time

System\Processor Queue Length

Memory\Available MBytes

Memory\Pages/sec

Memory\Committed Bytes

PhysicalDisk(*)\Avg. Disk Queue Length

PhysicalDisk(*)\Avg Disk sec/Read

PhysicalDisk(*)\Avg Disk sec/Write

Network Interface(*)\Bytes Total/sec

Process(*)\% Processor Time


If you master these 10 counters, you'll be ahead of many administrators and will be able to diagnose the majority of Windows Server performance issues in enterprise environments. Given your role supporting Windows Server upgrades, IIS applications, Capture servers, and enterprise workloads, PerfMon is one of the best tools you can add to your troubleshooting toolkit.
