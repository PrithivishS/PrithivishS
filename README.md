## Hi there 👋

<!--
**PrithivishS/PrithivishS** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

Linux Debugging 
Day 2 
----------
Core Linux Tracers: 
Enabling Ftrace --> Which .config to look for 
perf --> Profiling tool 
BPF --> Berkeley Packet Filter
bpftrace --->
BCC  --> 


Ways to collect data
Kprobes
Ftrace
   - trace-cmd
   - kernelshark
   - 
perf_events
LTTng Linux Trace Tools
   - 
eBPF 

Flame graph


Where is ltrace useful in debugging
- Multithreaded apps use the pthread library. Ltrace very useful for debugging multithreaded applications.
- Ltrace can give you times and counts of library functions that are being used by the application
   - giving a clue to which library call are taking lot of time and also bulk of time in % of time a function is comsuming.
   - So it is like a user space profiler
 

Strace: 


-->
Strace can show you that the linux loader i.e. ld.so memory maps the glibc for any running process into the processes address space to enable the direct library calling. 

Strace depends upon debugfs 
- To verify look at the path /sys/kernel/debug/tracing
- 

